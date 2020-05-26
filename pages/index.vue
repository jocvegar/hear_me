<template>
  <div>
    <b-container fluid class="pt-5">
      <b-row v-if="isConnected">
        <b-col cols="12" md="8" offset-md="2" class="pt-5">
          <h4 class="display-4 text-center">Escuchando de Spotify</h4>
          <br>
          <NowPlaying v-if="showTrack" :nowPlaying="track" :isPlaying="isPlaying"/>
        </b-col>
      </b-row>
      <b-row v-else>
        <p v-if="!isConnected">
          😭 {{ $nuxt.layout && $nuxt.layout.authorName }} hasn't connected yet. 😭
        </p>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import NowPlaying from '~/components/NowPlaying.vue'

export default {
  components: { NowPlaying },
  computed: {
    showTrack() {
      return this.isConnected && this.track
    },
    nowPlaying() {
      if (Boolean(Object.keys(this.$store.state.nowPlaying).length !== 0)) {
        this.$store.dispatch('updateConnection', true)
        return this.$store.state.nowPlaying
      }
      return this.$store.state.recentlyPlayed
    },
    track() {
      return this.nowPlaying
    },
    isPlaying() {
      return this.$store.state.isPlaying
    },
    isConnected() {
      return this.$store.state.isConnected
    }
  }
}
</script>

<style scoped>
h4 {
  margin-bottom: 1.3rem;
}
</style>
