<template>
	<div class="allpost">
		<div class="px-4 py-3">
			<div class="card col-12 col-lg-8 col-xl-6 mx-auto py-4">
				<h1></h1>
				<form @submit.prevent="submit">
					<div>
						<label for="title" class="sr-only">Titre</label>
						<input v-model="title" id="title" type="text" placeholder="Donner un titre à votre poste..." class="col-lg-8" />
					</div>
					<div class="flex">
						<div>
							<label for="content" class="sr-only">Contenu</label>
							<textarea v-model="content" id="content" placeholder="Décrivez votre poste..." maxlength="150" rows="3" class="mt-3 col-lg-8" />
						</div>
						<div class="flex items-center">
							<label for="attachment" class="sr-only">Pièce-jointe</label>
							<input type="file" ref="image" id="attachment" v-on:change="handleFileUpload()" />
						</div>
					</div>
					<div v-if="submitStatus == 'error_create'" class="alert">Veuillez tout remplir !</div>
					<div class="mt-3">
						<button name="send-post" class="btn px-4">
							<span v-if="submitStatus == 'loading'">Envoie...</span>
							<span v-else>Publier</span>
						</button>
					</div>
				</form>
			</div>
		</div>
		<div class="col-12 col-lg-8 col-xl-8 mx-auto my-3 py-4">
			<div v-for="(post, id) in posts.slice().reverse()" class="flex" :key="id">
				<div class="card col-12 col-lg-8 col-xl-6 mx-auto my-5 bg-white py-4">
					<div class="ml-lg-3 align-items-center d-flex flex-row">
						<img
							v-if="
								users
									.map((user) => {
										if (user.id === post.UserId) return user.avatar;
									})
									.join('') !== (null || '')
							"
							:src="
								users
									.map((user) => {
										if (user.id === post.UserId) return user.avatar;
									})
									.join('')
							"
							alt="avatar"
							class="avatar rounded-circle"
						/>
						<img v-else src="../assets/defaultavatar.png" alt="avatar" class="align-items-center avatar rounded-circle" />
						<div class="ml-3 d-flex justify-content-start">{{ post.userName }}</div>
						<div class="ml-auto mr-2 d-flex justify-content-end">{{ dateTime(post.createdAt) }}</div>
						<button v-if="user.id == post.UserId || user.isAdmin == 1" @click="deletePost(post)" name="delete" class="btn d-flex justify-content-end">x</button>
					</div>
					<div>
						<h2 class="text-center py-2">{{ post.title }}</h2>
						<div class="flex align-center justify-center">
							<img
								class="w-100"
								id="post_img"
								v-if="post.attachment !== '' && post.attachment !== null && (post.attachment.split('.')[2] === 'gif' || 'png' || 'jpg')"
								:src="post.attachment"
								alt="image-video"
							/>
						</div>
						<p class="py-2">{{ post.content }}</p>
					</div>
					<div>
						<router-link :to="`/post/${post.id}`" class="btn">Lire les commentaires</router-link>
					</div>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
import { mapState } from "vuex";
import axios from "axios";
import moment from "moment";
export default {
	name: "AllPost",
	data: function () {
		return {
			title: "",
			content: "",
			attachment: null,
			submitStatus: null,
		};
	},
	computed: {
		...mapState({
			user: "userInfos",
			users() {
				return this.$store.state.users;
			},
			posts() {
				return this.$store.state.posts;
			},
		}),
	},
	methods: {
		dateTime(value) {
			return moment(value).format("DD-MM-YYYY");
		},
		handleFileUpload() {
			this.attachment = this.$refs.image.files[0];
		},
		submit() {
			const fd = new FormData();
			if (this.attachment != null || "") {
				fd.append("image", this.attachment, this.attachment.filename);
				fd.append("title", this.title);
				fd.append("content", this.content);
				fd.append("user", this.user);
			} else {
				fd.append("title", this.title);
				fd.append("content", this.content);
				fd.append("user", this.user);
			}
			this.submitStatus = "loading";
			axios
				.post("http://localhost:3000/api/posts/new", fd)
				.then((response) => {
					this.title = response.data;
					this.content = response.data;
					this.attachment = response.data;
					this.$router.go("/");
				})
				.catch((error) => ((this.submitStatus = "error_create"), console.log(error)));
		},

		deletePost: function (post) {
			let response = confirm("Êtes-vous sûr de vouloir supprimer ce post ? ");
			if (response) {
				this.$store.dispatch("deletePost", post);
				this.$router.go("/");
				return;
			}
		},
	},
};
</script>

<style scoped>
.alert {
	color: #b12f38;
}
.avatar {
	width: 50px;
	height: 50px;
}
.btn {
	background-color: #192946;
	color: white;
}
textarea {
	resize: none;
}
</style>
