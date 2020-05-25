<template>
	<div>
		<transition name="fade" mode="out-in">
		
			<b-container class="pt-5">
				<b-row>
					<b-col cols="8" offset="2">
						<b-card bg-variant="secondary" text-variant="dark" header="ESTAMOS?" class="text-center">
							<b-card-text>{{message}}</b-card-text>
							<b-button variant="info" nuxt-link to="/" name="home" :aria-current="'/' === $nuxt.$route.path ? 'page' : false">
								Vamonos
							</b-button>
						</b-card>
					</b-col>
				</b-row>
			</b-container>
		</transition>

	</div>
</template>

<script>
export default {
	computed: {
		isConnected() {
			return this.$store.state.isConnected
		},
		message() {
			return this.$store.state.message
		}
	},
	asyncData({ query }) {
		const spotifyId = process.env.SPOTIFY_CLIENT_ID
		const clientUrl = process.env.CLIENT_URL
		const spotifyUrl = `https://accounts.spotify.com/authorize?client_id=${spotifyId}&response_type=code&scope=user-read-currently-playing,user-read-recently-played&redirect_uri=${clientUrl}/api/spotify/callback`
		return {
			spotifyUrl,
			query
		}
	},
	mounted() {
		if (
			!Boolean(this.query.success || this.query.error) &&
			!Boolean(this.isConnected)
		) {
			window.location = this.spotifyUrl
		} else if (Boolean(Object.keys(this.query).length !== 0)) {
			window.history.replaceState({}, document.title, window.location.pathname)
			this.$store.commit(
				'updateMessage',
				this.query.success || this.query.error
			)
			if (Boolean(this.query.success)) {
				this.$store.dispatch('updateConnection', true)
			}
		}
		if (Boolean(this.isConnected)) {
			this.$store.commit('updateMessage', "We're Connected Papi Joc")
		}
	}
}
</script>

<style scoped>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 600ms ease-out;
}

.fade-enter,
.fade-leave-active {
  opacity: 0;
}
</style>
