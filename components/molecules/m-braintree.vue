<template>
  <div class="braintree" id="braintree" />
</template>

<script>
import config from 'config'
import { currentStoreView } from '@vue-storefront/core/lib/multistore'

export default {
  name: 'BraintreeDropin',
  data () {
    const storeView = currentStoreView()
    return {
      loader: false,
      commit: true,
      nonce: '',
      currency: storeView.i18n.currencyCode,
      locale: storeView.i18n.defaultLocale.replace('-', '_') // Convert to PayPal format of locale
    }
  },
  mounted () {
    this.configureBraintree()
  },
  computed: {
    paymentDetails () {
      let paymentDetails = this.$store.getters['checkout/getPaymentDetails']
      return paymentDetails
    },
    grandTotal () {
      let cartTotals = this.$store.getters['cart/getTotals']
      return cartTotals.find(seg => seg.code === 'grand_total').value
    }
  },
  methods: {
    configureBraintree () {
      var self = this
      this.$store.dispatch('braintree/generateToken').then((resp) => {
        var dropin = require('braintree-web-drop-in')
        console.debug('Code for braintree:' + resp)
        var button = document.querySelector('.braintree-place-order-btn')
        dropin.create({
          authorization: resp,
          container: '#braintree',
          card: {
            overrides: {
              fields: {
                postalCode: {
                  prefill: this.paymentDetails.zipCode
                }
              }
            }
          },
          paypal: {
            flow: 'checkout',
            amount: this.getTransactions().amount.total,
            currency: this.getTransactions().amount.currency
          },
          googlePay: {
            googlePayVersion: 2,
            merchantId: config.braintree.googleMerchantId,
            transactionInfo: {
              totalPriceStatus: 'FINAL',
              totalPrice: String(this.getTransactions().amount.total),
              currencyCode: this.getTransactions().amount.currency
            },
            allowedPaymentMethods: [{
              type: 'CARD',
              parameters: {
                billingAddressRequired: true,
                billingAddressParameters: {
                  format: 'FULL'
                }
              }
            }]
          },
          applePay: {
            displayName: config.braintree.displayName,
            paymentRequest: {
              total: {
                label: config.braintree.displayName,
                amount: String(this.getTransactions().amount.total)
              },
              requiredBillingContactFields: ["postalAddress"]
            }
          }
        }).then((dropinInstance) => {
          button.addEventListener('click', () => {
            if (dropinInstance.isPaymentMethodRequestable()) {
              setTimeout(() => {
                dropinInstance.requestPaymentMethod((err, payload) => {
                  if (!err) {
                    console.debug(payload)
                    // Submit payload.nonce to your server
                    self.nonce = payload.nonce
                    console.error('success')
                    // when payment made through 'paypal through braintree' update payment method to 'braintree_paypal'
                    if(payload.type === "PayPalAccount"){
                      self.$store.state.checkout.paymentDetails.paymentMethod="braintree_paypal"
                    }
                    if(payload.type === "AndroidPayCard"){
                      self.$store.state.checkout.paymentDetails.paymentMethod="braintree_googlepay"
                    }
                    if(payload.type === "ApplePayCard"){
                      self.$store.state.checkout.paymentDetails.paymentMethod="braintree_applepay"
                    }
                    self.$bus.$emit('checkout-do-placeOrder', {
                      payment_method_nonce: self.nonce
                    })
                  } else {
                    console.error(err)
                  }
                }).catch((requestPaymentMethodErr) => {
                  // No payment method is available.
                  // An appropriate error will be shown in the UI.
                  console.error(requestPaymentMethodErr)
                })
              }, 400)
            }
          })
        }).catch((error) => {
          console.error(error)
        })
      }).catch((error) => {
        console.error(error)
      })
    },
    getTransactions () {
      return { amount: { total: this.grandTotal, currency: this.currency } }
    },
    getNonce () {
      return { nonce: this.nonce, total: this.grandTotal, currency: this.currency }
    },
    doPayment (data, actions) {
      return this.$store.dispatch('braintree/doPayment', this.getNonce())
    },
    onAuthorize (data, actions) {
      return true
    },
    onCancel (data) {
      this.$emit('payment-braintree-cancelled', data)
    }
  }
}
</script>