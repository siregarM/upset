<template>
    <div class="container">
      <form v-on:submit="sumbitArticleEdit()">
          <div class="form-group">
            <label for="judul">Judul:</label>
            <input type="text" class="form-control" id="judul" v-model="articles.judul">
          </div>
          <div class="form-group">
            <label for="isi">Isi:</label>
            <textarea class="form-control" id="isi" rows="5" v-model="articles.isi"></textarea>
          </div>
          <button class="btn btn-primary">Submit</button>
    </form>
    </div>
</template>

<script>

export default {
  data() {
    return {
      articles: {
        judul : '',
        isi : '',
      },
      errors: []
    }
  },

  created() {
    let id = this.$route.params.id;
    axios.get('/articles/' + id +  '/edit')
    .then(response => {
      // JSON responses are automatically parsed.
      this.articles = response.data
    })
    .catch(e => {
      this.errors.push(e)
    })
  },

  // Fetches posts when the component is created.
  methods: {
    sumbitArticleEdit() {
    let id = this.$route.params.id;
    axios.patch('/articles/' + id, this.articles)
    .then(response => {
      // JSON responses are automatically parsed.
      console.log(response);
      this.$router.push({path: '/'});
      this.articles = response.data
    })
    .catch(e => {
      this.errors.push(e)
    })
  }
  }
}
</script>

