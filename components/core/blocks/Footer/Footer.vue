<template>
  <footer :class="{ 'brdr-top-1 brdr-cl-secondary': isCheckoutPage }">
    <newsletter class=" flex brdr-bottom-1 brdr-cl-secondary" v-if="!isCheckoutPage" />
    <div
      class="footer-links flex pt30 pb60 px40 bg-cl-secondary"
      v-if="!isCheckoutPage"
    >
      <div class="container">
        <div class="row m0 center-xs between-md">
          <div
            class="row m0 col-lg-7 col-md-8 col-xs-12 start-md between-md between-xs no-mobile"
          >
          </div>
          <div class="row social mt30">
            <a
              class="social-icon mx10 brdr-circle no-underline"
              href="https://www.facebook.com/enthrallrecords"
              :aria-label="$t('Go to Facebook')"
            >
              <svg xmlns="http://www.w3.org/2000/svg" class="facebook icon" width="40" height="40" viewBox="0 0 40 40" fill="#BDBDBD">
                <path d="M20,0 C8.9541,0 0,8.95435 0,20 C0,31.0457 8.9541,40 20,40 C31.0459,40 40,31.0457 40,20 C40,8.95435 31.0459,0 20,0 Z M22.085,20.8785 L22.085,31.7595 L17.5825,31.7595 L17.5825,20.8789 L15.3335,20.8789 L15.3335,17.1293 L17.5825,17.1293 L17.5825,14.8779 C17.5825,11.819 18.8525,10 22.4609,10 L25.4653,10 L25.4653,13.7501 L23.5874,13.7501 C22.1826,13.7501 22.0898,14.2742 22.0898,15.2521 L22.085,17.1288 L25.4863,17.1288 L25.0884,20.8785 L22.085,20.8785 Z"/>
              </svg>
            </a>
            <a
              class="social-icon mx10 brdr-circle no-underline"
              href="https://www.instagram.com/enthrallrecords"
              :aria-label="$t('Go to Instagram')"
            >
              <svg xmlns="http://www.w3.org/2000/svg" class="instagram icon" width="40" height="40" viewBox="0 0 40 40" fill="#BDBDBD">
                <path d="M20,0 C8.9541,0 0,8.95435 0,20 C0,31.0457 8.9541,40 20,40 C31.0459,40 40,31.0457 40,20 C40,8.95435 31.0459,0 20,0 Z M15.603,9.39783 C16.7407,9.34607 17.104,9.33337 20.001,9.33337 C22.8955,9.33337 23.2578,9.34607 24.3955,9.39783 C25.5312,9.44983 26.3066,9.62964 26.9868,9.89343 C27.689,10.1656 28.2822,10.53 28.8755,11.1234 C29.4692,11.7163 29.8335,12.3114 30.1069,13.0129 C30.3691,13.6912 30.5488,14.4663 30.6025,15.6019 C30.6533,16.7396 30.667,17.1033 30.667,20.0001 C30.667,22.8971 30.6533,23.2598 30.6025,24.3976 C30.5488,25.5327 30.3691,26.308 30.1069,26.9865 C29.8335,27.6877 29.4692,28.283 28.8755,28.8759 C28.2832,29.4691 27.689,29.8345 26.9873,30.1069 C26.3086,30.3707 25.5327,30.5505 24.397,30.6025 C23.2593,30.6543 22.897,30.6669 20,30.6669 C17.103,30.6669 16.7397,30.6543 15.6021,30.6025 C14.4668,30.5505 13.6914,30.3707 13.0127,30.1069 C12.3115,29.8345 11.7163,29.4691 11.1235,28.8759 C10.5308,28.283 10.166,27.6877 9.89355,26.9862 C9.62988,26.308 9.4502,25.5328 9.39795,24.3973 C9.34619,23.2595 9.3335,22.8971 9.3335,20.0001 C9.3335,17.1033 9.34668,16.7395 9.39795,15.6017 C9.44873,14.4666 9.62891,13.6912 9.89307,13.0127 C10.1665,12.3114 10.5312,11.7163 11.1245,11.1234 C11.7173,10.5303 12.3125,10.1658 13.0142,9.89343 C13.6924,9.62964 14.4673,9.44983 15.603,9.39783 Z"/>
                <path d="M7.7876,1.2868e-05 L8.74463,1.2868e-05 C11.5928,1.2868e-05 11.9302,0.0102668 13.0547,0.0612922 C14.0947,0.1089 14.6592,0.282606 15.0352,0.428724 C15.5332,0.621961 15.8882,0.853162 16.2612,1.22645 C16.6343,1.59974 16.8657,1.95534 17.0591,2.45314 C17.2051,2.82875 17.3794,3.3932 17.4268,4.43312 C17.4775,5.55763 17.4888,5.8954 17.4888,8.74208 C17.4888,11.5888 17.4775,11.9265 17.4268,13.051 C17.3789,14.0911 17.2051,14.6555 17.0591,15.031 C16.8657,15.5288 16.6343,15.8833 16.2612,16.2564 C15.8877,16.6298 15.5332,16.8609 15.0352,17.0542 C14.6597,17.2008 14.0947,17.3742 13.0547,17.4218 C11.9302,17.4728 11.5928,17.4839 8.74463,17.4839 C5.89648,17.4839 5.55859,17.4728 4.43408,17.4218 C3.39404,17.3738 2.82959,17.2 2.45361,17.054 C1.95557,16.8606 1.6001,16.6295 1.22705,16.2561 C0.853516,15.8828 0.622559,15.5282 0.428711,15.0302 C0.282715,14.6546 0.108887,14.0901 0.0615234,13.0502 C0.0102539,11.9257 0,11.5879 0,8.73939 C0,5.891 0.0102539,5.55494 0.0615234,4.43043 C0.108887,3.39052 0.282715,2.82606 0.428711,2.44996 C0.62207,1.95228 0.853516,1.59669 1.22705,1.22328 C1.6001,0.849988 1.95557,0.618909 2.45361,0.425062 C2.82959,0.278455 3.39404,0.105115 4.43408,0.0573859 C5.41846,0.0128303 5.7998,-0.000475413 7.7876,1.2868e-05 Z M14.438,1.77113 C13.7314,1.77113 13.1582,2.34376 13.1582,3.05067 C13.1582,3.75734 13.7314,4.3307 14.438,4.3307 C15.145,4.3307 15.7183,3.75734 15.7183,3.05067 C15.7183,2.34401 15.145,1.77064 14.438,1.77113 Z M3.2666,8.74452 C3.2666,5.71937 5.71924,3.26674 8.74463,3.26674 C11.7695,3.26674 14.2212,5.71937 14.2212,8.74452 C14.2212,11.7697 11.7695,14.2213 8.74463,14.2213 C5.71924,14.2213 3.2666,11.7697 3.2666,8.74452 Z" transform="translate(11.26 11.26)"/>
                <path stroke="#FFF" stroke-width="2" d="M4.55499342,0 C7.07049549,0 9.10999966,2.03920952 9.10999966,4.55499342 C9.10999966,7.07049549 7.07049549,9.10999966 4.55499342,9.10999966 C2.03920952,9.10999966 0,7.07049549 0,4.55499342 C0,2.03920952 2.03920952,2.02282451e-15 4.55499342,2.02282451e-15 L4.55499342,0 Z" transform="translate(15.45 15.44)"/>
              </svg>
            </a>
            <a
              class="social-icon mx10 brdr-circle no-underline"
              href="https://www.twitter.com/enthrallrecords"
              :aria-label="$t('Go to Twitter')"
            >
              <svg xmlns="http://www.w3.org/2000/svg" class="twitter icon" width="40" height="40" viewBox="0 0 40 40" fill="#BDBDBD">
                <path d="M 40,20 C 40,31.05 31.05,40 20,40 8.95,40 0,31.05 0,20 0,8.95 8.95,0 20,0 31.05,0 40,8.95 40,20 Z M 16.34,30.55 c 8.87,0 13.72,-7.35 13.72,-13.72 0,-0.21 0,-0.42 -0.01,-0.62 0.94,-0.68 1.76,-1.53 2.41,-2.5 -0.86,0.38 -1.79,0.64 -2.77,0.76 1,-0.6 1.76,-1.54 2.12,-2.67 -0.93,0.55 -1.96,0.95 -3.06,1.17 -0.88,-0.94 -2.13,-1.52 -3.52,-1.52 -2.66,0 -4.82,2.16 -4.82,4.82 0,0.38 0.04,0.75 0.13,1.1 -4.01,-0.2 -7.56,-2.12 -9.94,-5.04 -0.41,0.71 -0.65,1.54 -0.65,2.42 0,1.67 0.85,3.15 2.15,4.01 -0.79,-0.02 -1.53,-0.24 -2.18,-0.6 0,0.02 0,0.04 0,0.06 0,2.34 1.66,4.28 3.87,4.73 -0.4,0.11 -0.83,0.17 -1.27,0.17 -0.31,0 -0.61,-0.03 -0.91,-0.09 0.61,1.92 2.39,3.31 4.5,3.35 -1.65,1.29 -3.73,2.06 -5.99,2.06 -0.39,0 -0.77,-0.02 -1.15,-0.07 2.11,1.38 4.65,2.18 7.37,2.18"/>
              </svg>
            </a>
          </div>
        </div>
      </div>
    </div>
    <div class="container">
      <div class="row middle-xs px15 bottom-links">
        <div class="col-xs-5 col-sm-3 cl-tertiary">
          <language-switcher v-if="multistoreEnabled" />
        </div>
        <div class="col-xs col-sm-9 end-xs">
          <ul class="pl0 links" data-testid="bottomLinks">
            <li class="footer__version-info">
              {{ getVersionInfo }}
            </li>
            <li class="inline-flex">
              <router-link
                class="cl-tertiary underline"
                to="/privacy"
                exact
              >
                {{ $t('Privacy policy') }}
              </router-link>
            </li>
          </ul>
        </div>
      </div>
    </div>
    <back-to-top bottom="20px" right="20px" visibleoffset="200">
      <button type="button" class="btn-top button no-outline brdr-none cl-white bg-cl-mine-shaft :bg-cl-th-secondary py10 px10">
        <svg width="24" height="24" xmlns="http://www.w3.org/2000/svg" fill-rule="evenodd" clip-rule="evenodd">
          <path d="M23.245 20l-11.245-14.374-11.219 14.374-.781-.619 12-15.381 12 15.391-.755.609z" fill="white" />
        </svg>
      </button>
    </back-to-top>
  </footer>
</template>

<script>
import { mapGetters } from 'vuex'
import { currentStoreView, localizedRoute } from '@vue-storefront/core/lib/multistore'
import CurrentPage from 'theme/mixins/currentPage'
import LanguageSwitcher from '../../LanguageSwitcher.vue'
import Newsletter from 'theme/components/core/blocks/Footer/Newsletter'
import BackToTop from 'theme/components/core/BackToTop'
import { getPathForStaticPage } from 'theme/helpers'
import config from 'config'

export default {
  mixins: [CurrentPage],
  name: 'MainFooter',
  methods: {
    goToAccount () {
      this.$bus.$emit('modal-toggle', 'modal-signup')
    },
    getLinkFor (path) {
      return localizedRoute(getPathForStaticPage(path))
    }
  },
  computed: {
    ...mapGetters({
      isLogged: 'user/isLoggedIn'
    }),
    multistoreEnabled () {
      return config.storeViews.multistore
    },
    getVersionInfo () {
      return `v${process.env.__APPVERSION__} ${process.env.__BUILDTIME__}`
    }
  },
  components: {
    Newsletter,
    LanguageSwitcher,
    BackToTop
  }
}
</script>

<style lang="scss" scoped>
@import '~theme/css/variables/colors';
@import '~theme/css/helpers/functions/color';
$color-secondary: color(secondary);

.icon {
  transition: 0.3s all;
}

.social-icon {
  width: 40px;
  height: 40px;
  &:hover,
  &:focus,
  &:active {
    .icon {
      fill: $color-secondary;
    }
  }
}
.links {
  list-style-type: none;
  display: flex;
  flex-direction: column-reverse;
  align-items: flex-end;

  @media (min-width: 768px) {
    flex-direction: row;
    justify-content: flex-end;
    align-items: center;
  }
}

.bottom-links {
  @media (max-width: 767px) {
    padding: 0;
  }
}

.footer__version-info {
  display: flex;
  color: $color-secondary;
  font-size: 0.7rem;
  @media (min-width: 768px) {
    margin-right: 1rem;
    font-size: 0.8rem;
  }
}

.underline {
  &:hover {
    color: $color-secondary;
    &:after {
      background-color: $color-secondary;
    }
  }
}
.legal-entity-link {
  text-align: center;
  @media (min-width: 768px) {
    display: none;
  }
}

.privacy-policy-link {
  text-align: right;
  @media (min-width: 768px) {
    display: none;
  }
}

@media (max-width: 595px) {
  .no-mobile {
    display: none;
  }

  .social {
    margin-top: 0;
  }

  .footer-links {
    padding-bottom: 30px;
  }
}
</style>
