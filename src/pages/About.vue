<template>
  <Layout>
    <main>
      <header class="max-w-xl md:max-w-2xl xl:max-w-3xl mx-auto text-center px-6 pt-24">
        <h1 class="text-4xl sm:text-5xl md:text-6xl font-sans font-bold mb-1">About</h1>
        <p class="text-grey-dark text-lg sm:text-3xl">Lorem ipsum subtitle &hellip;</p>
      </header>
      <nav class="absolute top-0 left-0 z-20 mt-6 ml-6">
        <g-link to="/" class="text-gray-900 border-gray-400 text-sm border opacity-75 hover:opacity-100 rounded-full px-4 py-2 transition-opacity">&larr; Home</g-link>
      </nav>
      <article class="max-w-xl md:max-w-2xl xl:max-w-3xl mx-auto px-6 sm:px-12 pt-16 border-b border-gray-300 pb-10 mb-16">
        <div class="markdown text-lg leading-normal text-gray-700">
          <hr>
          <p>Now what are the po</p>
          <h2>Community</h2>
          <p>Assemble a team.</p>
          <h2>Another heading</h2>
          <p>Something</p>
        </div>
      </article>
      <site-footer class="pb-8 sm:pb-10" />
    </main>
  </Layout>
</template>

<script>
import config from '~/.temp/config.js'
import SiteFooter from '@/components/Footer'

export default {
  components: {
    SiteFooter
  },
  metaInfo () {
    return {
      title: 'About',
      meta: [
        {
          key: 'description',
          name: 'description',
          content: 'Introduction to the Bleda blog starter for Gridsome.'
        },

        { property: "og:type", content: 'article' },
        { property: "og:title", content:'About' },
        { property: "og:description", content: 'Introduction to the Bleda blog starter for Gridsome.' },
        { property: "og:url", content: `${this.config.siteUrl}/about/` },
        { property: "og:image", content: '/images/bleda-card.png' },

        { name: "twitter:card", content: "summary_large_image" },
        { name: "twitter:title", content: 'About' },
        { name: "twitter:description", content: 'Introduction to the Bleda blog starter for Gridsome.' },
        { name: "twitter:site", content: "@cossssmin" },
        { name: "twitter:creator", content: "@cossssmin" },
        { name: "twitter:image", content: '/images/bleda-card.png' },
      ],
    }
  },
  computed: {
    config () {
      return config
    },
  },
}
</script>
