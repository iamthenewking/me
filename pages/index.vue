<template>
  <div id="home-page" class="page-wrapper home-page">
    <site-hero :title="$siteConfig.tagLine" image="/uploads/home-hero.jpg">
      <button
        v-if="$siteConfig.newsletter.on"
        class="button is-primary"
        @click="$eventBus.$emit('modal-triggered', 'newsletter-modal')"
      >
        Subscribe to my newsletter
      </button>
    </site-hero>
    <main-section theme="sidebar-right">
      <template v-slot:default>
        <p class="title">
          Latest content
        </p>
        <posts-grid :per-row="2" :number="4" />

        <p class="content has-text-centered">
          <a class="button is-primary is-outlined" href="/categories">
            More posts
          </a>
        </p>
        <p class="title">
          Browse by category
        </p>
        <categories-grid :per-row="3" />
      </template>

      <template v-slot:sidebar>
        <div class="content has-text-centered">
            <social-media />
            <br/>
          <p class="is-size-7 is-size-6-widescreen is-size-6-mobile">
         <img src="/VB-LOG-R-2T.png">
          </p>
         

          
          
        </div>
      </template>
    </main-section>
    <news-letter-form-modal />
  </div>
</template>

<script>
import { mapState } from 'vuex'
import { setPageData, loadPageWidgets } from '../helper'
import NewsLetterFormModal from '~/components/NewsLetterFormModal'
import SocialMedia from '~/components/SocialMedia'

export default {
  name: 'HomePage',
  head() {
    return {
      title: `Home | ${this.$siteConfig.siteName}`
    }
  },
  components: {
    NewsLetterFormModal,
    SocialMedia
  },
  computed: {
    ...mapState(['title', 'subtitle', 'featureImage'])
  },
  fetch({ store, params }) {
    setPageData(store, { slug: 'home' })
  },
  mounted() {
    loadPageWidgets()
  }
}
</script>

<style>
.home-page .under-subtitle {
  border-top: none;
}

.image.profile {
  max-width: 156px;
  margin: auto;
}

.twitter-tweet {
  padding-top: 1em;
  margin-left: auto;
  margin-right: auto;
}
</style>
