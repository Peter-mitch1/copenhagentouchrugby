<template>
  <Layout>
    <main>
      <header class="flex">
        <div class="px-8 py-12 mx-auto max-w-md sm:max-w-xl lg:max-w-full lg:w-1/2 lg:py-24 px-12">
          <div class="xl:max-w-lg xl:ml-auto">
            <div class="flex">
              <div class="flex-initial">
                <div class="mt-4 h-16 w-16">
                  <g-image src="~/assets/logo.svg"
                    width="200" alt="Copenhagen Touch Rugby"
                    class="h-24 w-24 object-contain"/>
                </div>
              </div>
              <div class="flex-initial">
                <h1 class="ml-4 mt-6 text-3xl md:text-5xl font-bold text-gray-900 leading-tight">
                  <g-link to="/" class="uppercase">Copenhagen Touch</g-link>
                </h1>
              </div>
            </div>
            <g-image src="~/assets/images/home/touch.jpg" width="1000" class="mt-6 sm:mt-8 rounded-lg shadow-xl sm:h-64 sm:w-full sm:object-cover sm:object-center lg:hidden" alt ="Playing field"/>
            <h2 class="mt-6 sm:mt-8 text-2xl sm:text-4xl lg:text-5xl font-bold text-gray-900 leading-tight">Burn fat without trying
              <span class="text-indigo-500">while socialising</span>
            </h2>
            <div class="text-gray-600 sm:text-xl">
              <p class="mt-2 sm:mt-4">
                Touch rugby encourages socialising and keeping the game as up-beat as possible, but it's the improvements on fitness that really stand out.
              </p>
              <p class="mt-2 sm:mt-4">
                It's great way to improve your cardio vascular fitness, raising and lowering your heart rate and burning fat at a pace that suits you.
              </p>
              <p class="mt-2 sm:mt-4">
                Touch rugby is a fantastic way to keep fit or get fit, without really thinking about it. It's a lot easier to play a game with your mates for an hour than run for an hour.
              </p>
            </div>
            <div class="mt-4 sm:mt-6">
              <a class="btn btn-indigo shadow-lg sm:text-base"
                href="https://www.facebook.com/groups/172852439436767/">
                join the group
              </a>
              <a href="#" class="ml-2 btn btn-gray sm:text-base">learn more</a>
            </div>
          </div>
        </div>
        <div class="hidden lg:block lg:w-1/2 lg:relative">
          <g-image src="~/assets/images/home/touch.jpg" width="1000" class="absolute inset-0 h-full w-full object-cover object-center" alt ="Playing field"/>
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

