<template>
  <div class="mb35">
    <!-- My profile header -->
    <div class="row mb15">
      <div class="col-xs-12 col-sm-6" :class="{ 'cl-accent' : !isEdited }">
        <h3 class="m0 mb5">
          {{ $t('My profile') }}
        </h3>
      </div>
      <div class="col-xs-12 col-sm-6">
        <div class="lh30 flex end-md" v-if="!isEdited">
          <a href="#" class="cl-tertiary flex" @click.prevent="edit">
            <span class="pr5">
              {{ $t('Edit your profile') }}
            </span>
            <i class="material-icons cl-tertiary">edit</i>
          </a>
        </div>
      </div>
    </div>

    <!-- My profile body (edit mode) -->
    <div class="row" v-if="isEdited">
      <base-input
        class="col-xs-12 col-md-6 mb10"
        type="text"
        name="first-name"
        autocomplete="given-name"
        :placeholder="$t('First name')"
        v-model.trim="currentUser.firstname"
        @input="$v.currentUser.firstname.$touch()"
        :validations="[
          {
            condition: !$v.currentUser.firstname.required,
            text: $t('Field is required')
          },
          {
            condition: !$v.currentUser.firstname.minLength,
            text: $t('Name must have at least 2 letters.')
          }
        ]"
      />

      <base-input
        class="col-xs-12 col-md-6 mb10"
        type="text"
        name="last-name"
        autocomplete="family-name"
        :placeholder="$t('Last name')"
        v-model.trim="currentUser.lastname"
        @input="$v.currentUser.lastname.$touch()"
        :validations="[{
          condition: !$v.currentUser.lastname.required,
          text: $t('Field is required')
        }]"
      />

      <base-input
        class="col-xs-12 col-md-6 mb10"
        type="email"
        name="email-address"
        autocomplete="email"
        :placeholder="$t('Email address')"
        v-model="currentUser.email"
        :validations="[
          {
            condition: !$v.currentUser.email.required,
            text: $t('Field is required')
          },
          {
            condition: !$v.currentUser.email.email,
            text: $t('Please provide valid e-mail address.')
          }
        ]"
      />

      <!-- Change password (edit mode) -->
      <base-checkbox
        class="col-xs-12 mb15"
        id="changePassword"
        v-model="changePassword"
      >
        {{ $t('Change my password') }}
      </base-checkbox>

      <template v-if="changePassword">
        <base-input
          class="col-xs-12 col-md-6 mb15 mt10"
          type="password"
          name="old-password"
          autocomplete="current-password"
          :placeholder="$t('Current password *')"
          v-model="oldPassword"
          @input="$v.oldPassword.$touch()"
          :validations="[{
            condition: !$v.oldPassword.required && $v.oldPassword.$error,
            text: $t('Field is required')
          }]"
        />

        <div class="hidden-xs hidden-sm col-md-6 mb15 mt10" />

        <base-input
          class="col-xs-12 col-md-6 mb15 mt10"
          type="password"
          name="password"
          autocomplete="new-password"
          :placeholder="$t('New password *')"
          v-model="password"
          @input="$v.password.$touch()"
          :validations="[{
            condition: !$v.password.required && $v.password.$error,
            text: $t('Field is required')
          }]"
        />

        <base-input
          class="col-xs-12 col-md-6 mb15 mt10"
          type="password"
          name="password-confirm"
          autocomplete="new-password"
          :placeholder="$t('Repeat new password *')"
          v-model="rPassword"
          @input="$v.rPassword.$touch()"
          :validations="[
            {
              condition: !$v.rPassword.required && $v.rPassword.$error,
              text: $t('Field is required')
            },
            {
              condition: !$v.rPassword.sameAsPassword,
              text: $t('Passwords must be identical.')
            }
          ]"
        />
      </template>

      <div class="col-xs-12 col-sm-6">
        <button-full
          @click.native="updateProfile"
          :disabled="checkValidation()"
        >
          {{ $t('Update my profile') }}
        </button-full>
      </div>
      <div class="col-xs-12 col-sm-6 flex middle-xs py10">
        <a href="#" @click="exitSection" class="h4 cl-accent">
          {{ $t('Cancel') }}
        </a>
      </div>
    </div>

    <!-- My profile summary -->
    <div class="row fs16 mb35" v-else>
      <div class="col-xs-12 h4">
        <p>
          {{ currentUser.firstname }} {{ currentUser.lastname }}
        </p>
        <p>
          {{ currentUser.email }}
        </p>
      </div>
    </div>
  </div>
</template>

<script>
import { required, minLength, email, sameAs } from 'vuelidate/lib/validators'
import MyProfile from '@vue-storefront/core/compatibility/components/blocks/MyAccount/MyProfile'
import { unicodeAlpha, unicodeAlphaNum } from '@vue-storefront/core/helpers/validators'

import BaseCheckbox from 'theme/components/core/blocks/Form/BaseCheckbox'
import BaseSelect from 'theme/components/core/blocks/Form/BaseSelect'
import BaseInput from 'theme/components/core/blocks/Form/BaseInput'
import ButtonFull from 'theme/components/theme/ButtonFull'
import Tooltip from 'theme/components/core/Tooltip'

export default {
  components: {
    BaseCheckbox,
    BaseSelect,
    BaseInput,
    ButtonFull,
    Tooltip
  },
  mixins: [MyProfile],
  computed: {
    countryOptions () {
      return this.countries.map((item) => {
        return {
          value: item.code,
          label: item.name
        }
      })
    }
  },
  methods: {
    checkValidation () {
      if (this.changePassword && this.addCompany) {
        return this.$v.$invalid
      } else if (this.changePassword && !this.addCompany) {
        return this.$v.currentUser.$invalid || this.$v.password.$invalid || this.$v.rPassword.$invalid
      } else if (!this.changePassword && this.addCompany) {
        return this.$v.currentUser.$invalid || this.$v.userCompany.$invalid
      } else {
        return this.$v.currentUser.$invalid
      }
    }
  },
  validations: {
    currentUser: {
      firstname: {
        required,
        minLength: minLength(2),
        unicodeAlpha
      },
      lastname: {
        required,
        unicodeAlpha
      },
      email: {
        required,
        email
      }
    },
    oldPassword: {
      required
    },
    password: {
      required
    },
    rPassword: {
      required,
      sameAsPassword: sameAs('password')
    },
    userCompany: {
      company: {
        required
      },
      country: {
        required
      },
      street: {
        required,
        unicodeAlphaNum
      },
      house: {
        required,
        unicodeAlphaNum
      },
      postcode: {
        required,
        minLength: minLength(3)
      },
      city: {
        required,
        unicodeAlpha
      },
      taxId: {
        required,
        minLength: minLength(3)
      }
    }
  }
}
</script>
