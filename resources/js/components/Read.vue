<template>
    <div class="container">
                <div class="card">
                    <div class="card-header">
                        <router-link to="/"><i class="fa fa-arrow-left"></i></router-link>
                    </div>

                    <div class="card-body">
                       <h1>{{articles.judul}}</h1>
                       <p>{{articles.isi}}</p>
                    </div>
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
    let id = this.$route.params.id;
    axios.get('/articles/' + id)
    .then(response => {
      // JSON responses are automatically parsed.
      this.articles = response.data
    })
    .catch(e => {
      this.errors.push(e)
    })
  }
}
</script>
