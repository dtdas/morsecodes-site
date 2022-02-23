<template>
  <v-container fluid>
    <v-row flex>
      <v-col md="4" v-for="article of articles" :key="article">
        <v-card>
          <nuxt-link :to="{ name: 'slug', params: { slug: article.slug } }">
            <v-card-title>{{ article.title }}</v-card-title>
            <v-card-text>{{ article.description }}</v-card-text>
          </nuxt-link>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  async asyncData({ $content, params }) {
    const articles = await $content('blog', params.slug)
      .only(['title', 'description', 'img', 'slug'])
      .sortBy('createdAt', 'asc')
      .fetch()
    return {
      articles,
    }
  },
}
</script>
