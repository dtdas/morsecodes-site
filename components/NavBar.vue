<template>
  <nav>
    <v-app-bar flat prominent>
      <nuxt-link to="/">
        <v-img
          max-height="110"
          max-width="256"
          :src="require('~/static/morselogo.png')"
        />
      </nuxt-link>
      <v-spacer></v-spacer>
      <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>
    </v-app-bar>
    <v-navigation-drawer v-model="drawer" absolute temporary right>
      <v-list>
        <v-list-item
          v-for="link in links"
          :key="link.text"
          nuxt-link
          :to="link.route"
        >
          <v-list-item-content>
            <v-list-item-title> {{ link.text }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
  </nav>
</template>

<script>
export default {
  data() {
    return {
      drawer: false,
      links: [
        { text: 'Home', route: '/' },
        { text: 'About', route: '/about' },
        { text: 'Blog', route: '/blog' },
      ],
    }
  },
}
</script>
