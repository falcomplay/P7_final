<template>
	<div class="post">
		<Navbar />
		<Post />
	</div>
</template>

<script>
import Navbar from "@/components/Navbar.vue";
import Post from "@/components/Post.vue";

export default {
	created() {
		this.$store.dispatch("getUsers");
		this.$store.dispatch("getUserInfos");
		this.$store.dispatch("getPostsInfos");
		this.$store.dispatch("getComments");
	},
	name: "Home",
	components: {
		Navbar,
		Post,
	},
};
</script>
