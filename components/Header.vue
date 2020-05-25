<template>
	<div>
		<b-navbar toggleable="lg" type="dark" variant="info">
			<b-navbar-brand nuxt-link to="/" name="Home">Music Me</b-navbar-brand>

			<b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

			<b-collapse id="nav-collapse" is-nav>
				<b-navbar-nav>
					<b-nav-item nuxt-link to="/about" name="about">About Me</b-nav-item>
				</b-navbar-nav>

				<!-- Right aligned nav items -->
				<b-navbar-nav v-if="isAuth" class="ml-auto">
					<b-nav-item nuxt-link to="/" name="Home">Back</b-nav-item>
				</b-navbar-nav>
				<b-navbar-nav v-if="!isAuth && !isConnected" class="ml-auto">
					<b-nav-item nuxt-link to="/auth" name="Home">Login</b-nav-item>
				</b-navbar-nav>
			</b-collapse>
		</b-navbar>
	</div>
</template>

<script>
export default {
	props: ['isAuth'],
	computed: {
		isConnected() {
			return this.$store.state.isConnected
		}
	}	
}
</script>
