<template>
  <div class="l-container--fixed s-default">
    <page-title class="text-center">
      <h1 slot="title" class="brand-pink-text"><i class="far fa-microphone-alt"></i> bettercast</h1>
    </page-title>

    <post-preview v-for="post in episodes" :key="post.permalink" :post="post" :showDate="true" />

    <nuxt-child></nuxt-child>
  </div>
</template>
<script>
import PostPreview from '~/components/PostPreview'
import PageTitle from '~/components/PageTitle'

export default {
  components: {
    PostPreview, PageTitle
  },

  async asyncData ({ app }) {
    let episodes = (await app.$content('bettercast').getAll()).filter((episode) => {
      return process.env.NODE_ENV === 'development' || !episode.draft
    })

    return {
      episodes
    }
  },

  head () {
    return {
      title: 'bettercast — better.co.at',
      meta: [
        { hid: 'description', name: 'description', content: 'Ein Podcast für Agile Entwicklung in Österreich' }
      ]
    }
  }
}
</script>
