<template>
  <div class="o-order-summary">
    <SfHeading
      :title="$t('Totals')"
      :level="3"
      class="sf-heading--left sf-heading--no-underline title"
    />
    <MPriceSummary :is-large="true" />
    <APromoCode :allow-promo-code-removal="false" />
    <div class="characteristics">
      <SfCharacteristic
        v-for="characteristic in characteristics"
        :key="characteristic.title"
        :title="characteristic.title"
        :description="characteristic.description"
        :icon="characteristic.icon"
        color-icon="green-primary"
        class="characteristics__item"
      />
    </div>
  </div>
</template>
<script>
import { SfHeading, SfCharacteristic } from '@storefront-ui/vue';
import APromoCode from 'theme/components/atoms/a-promo-code';
import MPriceSummary from 'theme/components/molecules/m-price-summary';
export default {
  name: 'OOrderSummary',
  components: {
    SfHeading,
    SfCharacteristic,
    APromoCode,
    MPriceSummary
  },
  data () {
    return {
      characteristics: [
        {
          title: this.$t('Easy shipping'),
          description: this.$t('You’ll receive confirmation of shipping and tracking info'),
          icon: 'shipping'
        }
      ]
    };
  }
};
</script>
<style lang="scss" scoped>
.title {
  --heading-title-margin: 0 0 var(--spacer-2xl) 0;
}
.property {
  margin: var(--spacer-base) 0;
}
.characteristics {
  margin: var(--spacer-xl) 0 0 var(--spacer-xs);
  &__item {
    margin: var(--spacer-base) 0;
  }
}
.actions {
  &__button {
    margin: var(--spacer-sm) 0;
    &--secondary {
      text-align: left;
    }
  }
}
</style>
