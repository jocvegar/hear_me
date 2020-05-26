<template>
  <div class="base">
    <Header :isAuth="isAuth"/>
      <nuxt/>
  </div>
</template>

<script>
import Header from '~/components/Header.vue'

export default {
  components: { Header },
  titleShort: 'escuchame',
  authorName: 'JoC',
  computed: {
    isAuth() {
      return this.$route.name === 'auth'
    },
    ariaCurrent() {
      return this.isAuth ? 'page' : false
    },
    rootClass() {
      return this.isAuth ? 'auth base' : 'base'
    }
  },
  head() {
    return {
      title: `${this.$options.authorName} ${
        this.$options.titleShort
      }`,
      link: [
        {
          rel: 'stylesheet',
          href: 'https://fonts.googleapis.com/css2?family=Chelsea+Market&display=swap'
        }
      ]
    }
  }
}
</script>

<style>
:root {
  --colorGray: #333642;
}
html {
  background: #000000;
}
body {
  padding: 0;
  margin: 0;
  color: white;
  font-family: 'Chelsea Market', cursive;
}
.base {
  background-size: cover;
  background-image: linear-gradient(to top, var(--colorGray), #000000);
  display: grid;
  grid-template-rows: auto 1fr auto;
  height: 100vh;
  overflow-x: hidden;
}
.nuxt-progress {
  opacity: 0.3;
  height: 2px;
  bottom: 0;
  top: auto;
}
</style>
