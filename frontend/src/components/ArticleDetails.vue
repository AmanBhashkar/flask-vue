<template>
	<div class = "container mt-5">
		<h2> {{articles.title}}</h2>
		<p class ="mt-3">
			{{articles.date}}
		</p>
	<router-link
	:to="{name:'articledit', params:{id:articles.id}}"
	class="btn btn-success mt-3"
	> Update</router-link>

	<button class="btn btn-danger mx-3 mt-3" @click="deleteArticle"> 
		Delete
	</button>
	</div>
</template>

<script>
export default {
	data() {
		return {
			articles: {}
		}
		
	},props: {
			id: {
				type:[Number,String],
				required: true
			}
		},
		methods:{
		deleteArticle() {
			fetch(`http://localhost:5000/delete/${this.id}/`, {
					method: "DELETE",
					headers: {
						'Content-Type': 'application/json;'
					},
				})

				.then(() => {
					this.$router.push({
						name:'home'
					})
				})
				.catch(error => {
					console.log(error)
				})
		

		},
		
		
		
		
		
		
		getArticlesData() {
			fetch(`http://localhost:5000/get/${this.id}/`, {
					method: "GET",
					headers: {
						'Content-Type': 'application/json;'
					}
				})
				.then(response => response.json())
				.then(data => {
					this.articles = data;

				})
				.catch(error => {
					console.log(error)
				})
		}
			},
		created() {
			this.getArticlesData()
		}

}
</script>

<style>

</style>