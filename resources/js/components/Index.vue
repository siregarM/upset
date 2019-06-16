<template>
	<div class="card">
		<div class="card-header">
			<h1 class="float-left">Article</h1>
			 <router-link to="/create" class="btn btn-success float-right">Create</router-link>
		</div>
		<div class="card-body">
			 <table class="table table-bordered">
			    <thead>
			      <tr>
			        <th>Judul</th>
			        <th>Isi</th>
			        <th width="300"></th>
			      </tr>
			    </thead>
			    <tbody>
			      <tr v-for="article, index in articles">
			        <td>{{article.judul}}</td>
			        <td>{{article.isi}}</td>
			        <td>
			        <router-link :to="{name : 'readArticle', params:{id:article.id}}" class="btn btn-info"> <i class="fa fa-eye"></i> Show</router-link>
			        <router-link :to="{name : 'editArticle', params:{id:article.id}}" class="btn btn-success"> <i class="fa fa-pencil"></i> Edit</router-link>
			        <button class="btn btn-danger" v-on:click="submitArticleDelete()"><i class="fa fa-trash"></i> Delete</button>
			        </td>
			      </tr>
			    </tbody>
			  </table>
		</div>
	</div>
</template>

<script>

export default {
  data() {
    return {
      articles: [],
      errors: []
    }
  },

  // Fetches articles when the component is created.
  created() {
    axios.get('/articles')
    .then(response => {
      // JSON responses are automatically parsed.
      this.articles = response.data
    })
    .catch(e => {
      this.errors.push(e)
    })
  },

  methods:{
  	submitArticleDelete(index, id){
  	axios.delete('/articles/' + id)
    .then(response => {
      // JSON responses are automatically parsed.
      this.articles.splice(index, 1)
    })
    .catch(e => {
      this.errors.push(e)
    })
  }
  }
}
</script>
