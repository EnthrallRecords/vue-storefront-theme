<template>
  <div id="page_not_found">
    <section class="bg-cl-secondary py35 px20">
      <div class="container">
        <h2>
          {{ $t("Something went wrong ...") }}
        </h2>
      </div>
    </section>
    <section class="bg-cl-primary py35 px20">
      <div class="container">
        <div class="lh16 h5 weight-400">
          <p>
            {{ $t("We noticed an error while handling your request.") }}
          </p>
          <p>
            {{ $t('If you need assistance you can drop us a line at') }}
            <a href="mailto:info@enthrallrecords.com" class="cl-secondary no-underline">
              {{ $t('contact mail') }}
            </a>
          </p>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
import Error from '@vue-storefront/core/pages/Error'

export default {
  name: 'Error',
  mixins: [Error]
}
</script>

<style scoped>
  a {
    text-decoration: underline;
  }
</style>
