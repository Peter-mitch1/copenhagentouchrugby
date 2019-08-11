<template>
  <Layout>
    <main>
      <header>
        <div class="px-8 py-12">
          <g-image src="~/assets/logo.svg" width="1000" alt="Copenhagen Touch Rugby"/>
          <h1 class="text-3xl">
            <g-link to="/" class="">Copenhagen Touch Rugby</g-link>
          </h1>
          <g-image src="~/assets/images/home/touch.jpg" width="1000" class="mt-6 rounded-lg shadow-xl" alt ="Playing field"/>
          <h2 class="mt-6 text-2xl font-bold text-gray-900 leading-tight">Get fit by having fun
            <span class="text-indigo-500">while socialising</span>
          </h2>
          <div class="text-gray-600">
            <p class="mt-2">
              Touch rugby encourages socialising and keeping the game as up-beat as possible, but it's the improvements on fitness that really stand out.
            </p>
            <p class="mt-2">
              It's great way to improve your cardio vascular fitness, raising and lowering your heart rate and burning fat at a pace that suits you.
            </p>
            <p class="mt-2">
              Touch rugby is a fantastic way to keep fit or get fit, without really thinking about it. It's a lot easier to play a game with your mates for an hour than run for an hour.
            </p>
          </div>
          <div class="mt-4">
            <a class="inline-block px-5 py-3 bg-indigo-500 text-sm text-white rounded-lg shadow-lg uppercase tracking-wider font-semibold" href="https://www.facebook.com/groups/172852439436767/">Join the group</a>
          </div>
        </div>
      </header>
      <section>
        <post-item v-for="edge in $page.posts.edges" :key="edge.node.id" :post="edge.node" />
      </section>
      <pagination :info="$page.posts.pageInfo" v-if="$page.posts.pageInfo.totalPages > 1" />
      <site-footer class="" />
    </main>
  </Layout>
</template>

<script>
import config from '~/.temp/config.js'
import SiteFooter from '@/components/Footer'
import PostItem from '@/components/PostItem'
import Pagination from '@/components/Pagination'

export default {
  components: {
    PostItem,
    Pagination,
    SiteFooter,
  },
  metaInfo () {
    return {
      title: this.config.siteName,
      meta: [
        { property: "og:type", content: 'website' },
        { property: "og:title", content: this.config.siteName },
        { property: "og:description", content: this.config.siteDescription },
        { property: "og:url", content: this.config.siteUrl },
        { property: "og:image", content: this.ogImageUrl },

        { name: "twitter:card", content: "summary_large_image" },
        { name: "twitter:title", content: this.config.siteName },
        { name: "twitter:description", content: this.config.siteDescription },
        { name: "twitter:site", content: "@cossssmin" },
        { name: "twitter:creator", content: "@cossssmin" },
        { name: "twitter:image", content: this.ogImageUrl },
      ],
    }
  },
  computed: {
    config () {
      return config
    },
    ogImageUrl () {
      return `${this.config.siteUrl}/images/bleda-card.png`
    }
  },
}
</script>

<page-query>
  query Home ($page: Int) {
    posts: allPost (page: $page, perPage: 6) @paginate {
      totalCount
      pageInfo {
        totalPages
        currentPage
      }
      edges {
        node {
          id
          title
          datetime: date (format: "YYYY-MM-DD HH:mm:ss")
          content
          excerpt
          description
          path
          cover
          tags {
            id
            title
            path
          }
          author {
            id
            title
            path
          }
        }
      }
    }
  }
</page-query>

