<template>
  <footer class="o-footer">
    <SfFooter :column="5" :multiple="true">
      <SfFooterColumn
        v-for="linkGroup in links"
        :key="linkGroup.name"
        :title="$t(linkGroup.name)"
      >
        <SfList>
          <SfListItem v-for="link in linkGroup.children" :key="link.name">
            <router-link v-if="link.link" :to="localizedRoute(link.link)" exact>
              <SfMenuItem class="sf-footer__menu-item" :label="$t(link.name)" />
            </router-link>
            <SfMenuItem
              v-else-if="link.clickHandler"
              class="sf-footer__menu-item"
              :label="$t(link.name)"
              @click="link.clickHandler"
            />
          </SfListItem>
        </SfList>
      </SfFooterColumn>
      <SfFooterColumn :title="$t('Info')">
        <SfList>
          <SfListItem>
            <router-link to="/privacy" exact>
              <SfMenuItem
                class="sf-footer__menu-item"
                :label="$t('Privacy policy')"
              />
            </router-link>
          </SfListItem>
          <SfListItem v-if="multistoreEnabled">
            <SfMenuItem
              @click.native="showLanguageSwitcher"
              class="sf-footer__menu-item"
              :label="currentLanguage"
            />
          </SfListItem>
          <SfListItem class="sf-footer__menu-item">
            {{ getVersionInfo }}
          </SfListItem>
        </SfList>
      </SfFooterColumn>
      <SfFooterColumn class="social-column">
        <div class="social-icon">
          <a
            :key="item.name"
            :href="item.link"
            v-for="item in social"
            class="social-icon__link"
          >
            <img
              :src="'/assets/icons/' + item.name + '.svg'"
              class="social-icon__img"
            >
          </a>
        </div>
      </SfFooterColumn>
    </SfFooter>
    <ABackToTop bottom="20px" right="20px" visibleoffset="200" class="desktop-only" />
  </footer>
</template>

<script>
import { mapActions, mapGetters } from 'vuex';
import ABackToTop from 'theme/components/atoms/a-back-to-top';
import { SfFooter, SfList, SfMenuItem } from '@storefront-ui/vue';
import { ModalList } from 'theme/store/ui/modals'
import { getPathForStaticPage } from 'theme/helpers';
import config from 'config';
import { currentStoreView } from '@vue-storefront/core/lib/multistore';
import get from 'lodash-es/get';

export default {
  name: 'OFooter',
  components: {
    ABackToTop,
    SfFooter,
    SfList,
    SfMenuItem
  },
  data () {
    return {
      social: [
        {name: 'facebook', link: 'https://www.facebook.com/enthrallrecords'},
        {name: 'twitter', link: 'https://www.twitter.com/enthrallrecords'},
        {name: 'instagram', link: 'https://www.instagram.com/enthrallrecords'},
        {name: 'youtube', link: 'https://www.youtube.com/c/Enthrallrecords/playlists'}
      ]
    };
  },
  computed: {
    ...mapGetters('user', ['isLoggedIn']),
    multistoreEnabled () {
      return get(config, 'storeViews.multistore', false);
    },
    getVersionInfo () {
      return `v${process.env.__APPVERSION__} ${process.env.__BUILDTIME__}`;
    },
    currentLanguage () {
      const { i18n = config.i18n } = currentStoreView();
      return `${i18n.defaultCountry} / ${i18n.defaultLanguage} / ${i18n.currencyCode}`;
    },
    links () {
      return {
        orders: {
          name: 'Orders',
          children: [
            {
              name: 'My account',
              ...this.isLoggedIn
                ? { link: '/my-account' }
                : { clickHandler: () => this.openModal({ name: ModalList.Auth, payload: 'login' }) }
            }
          ]
        }
      };
    }
  },
  methods: {
    ...mapActions('ui', {
      openModal: 'openModal'
    }),
    showLanguageSwitcher () {
      this.openModal({ name: ModalList.LanguageSwitcher })
    }
  }
};
</script>

<style lang="scss" scoped>
@import "~@storefront-ui/shared/styles/helpers/breakpoints";

.o-footer {
  @include for-desktop {
    max-width: 1272px;
    margin: auto;
  }
  .sf-footer {
    --footer-width: auto;
  }
}
.social-column {
  flex-basis: auto;
}
.social-icon {
  padding: var(--spacer-sm) var(--spacer-xl);
  @include for-desktop {
    padding: var(--spacer-xs) 0;
  }
  &__link {
    &:not(:last-child) {
      margin-right: var(--spacer-base);
    }
  }
  &__img {
    height: 1.75rem;
  }
}
</style>
