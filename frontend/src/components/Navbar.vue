<template>
	<div class="container-fluid px-0">
		<nav class="Navbar">
			<b-navbar toggleable="md" type="dark">
				<router-link :to="`/home`">
					<img class="navbar-brand img-fluid logo" src="../styles/icon/icon-font.png" aria-label="logo groupomania" alt="Logo groupomania" />
				</router-link>
				<b-navbar-toggle target="nav-collapse"></b-navbar-toggle>
				<b-collapse id="nav-collapse" is-nav>
					<b-navbar-nav class="ml-auto">
						<div class="d-flex justify-content-end align-items-center">
							<b-nav-item :href="'/profile'" class="mr-3 font-weight-bold">Mon Compte</b-nav-item>
							<span @click="logout()"><b-nav-item size="sm" class="mr-2 font-weight-bold">Se déconnecter</b-nav-item></span>
						</div>
					</b-navbar-nav>
				</b-collapse>
			</b-navbar>
		</nav>
	</div>
</template>

<script>
export default {
	methods: {
		logout: function () {
			this.$store.commit("logout");
			this.$router.push("/");
		},
	},
};
</script>

<style scoped>
img {
	width: 150px;
}
</style>
