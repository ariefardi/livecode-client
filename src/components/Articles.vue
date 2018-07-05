<template>
<body>

    <!-- Grid -->
<div class="w3-row topmg">
<!-- Blog entries -->
<div class="w3-col s12">
  <!-- Blog entry -->
  <div class="w3-card-4 w3-margin w3-white" v-for="(article, index) in articles" v-bind:key="index" >
    <img class="mrgntop" height="300px" width="1300px" :src="article.imgSrc" >
    <div class="w3-container">
      <h3><b> {{article.title}} </b></h3>
      <h5> <v-btn flat @click="getAuthor(article.author)" > {{article.author}} </v-btn> , <v-btn flat> <span class="w3-opacity"> {{article.category}} </span> </v-btn> </h5>
    </div>

    <div class="w3-container">
      <p> {{article.content}} </p>
        <div class="w3-row">
        <div class="w3-col m4">
          <v-btn v-if="article.author==userLogin"> Edit </v-btn>
          </div>
        <div class="w3-col m4">
         <v-btn @click="delArticle(index)" v-if="article.author==userLogin"> Delete </v-btn>
        </div>
      </div>
    </div>
  </div>
  <hr>
  </div>
  </div>
</body>
  <!-- Blog entry -->
</template>
<script>
import axios from 'axios'
export default{
  data () {
    return {
      articles: [],
      userLogin: localStorage.getItem('username')
    }
  },
  methods: {
    getArticles () {
      console.log('Jalan gak nih axiosnya')
      axios.get('http://localhost:3000/articles')
      .then(({data})=> {
        this.articles = data.dataArticles
        this.articles.reverse()
        // console.log(data.dataArticles)
        console.log(this.articles)
        console.log(this.userLogin)
      })
    },
    delArticle (index) {
      console.log('deleted',index)
      // console.log(this.articles[index]._id)
      let id = this.articles[index]._id
      this.articles.splice(index,1)
      axios.delete('http://localhost:3000/articles/delete/'+id)
      .then(()=>{
        swal('Article Deleted')
      })
    },
    getAuthor(item) {
      console.log(item)
      for(var i=0; i<this.articles.length;i++){
        if (this.articles[i].author!==item) {
          this.articles.splice(i,1)
        }
      }
    }
  },
  created () {
    this.getArticles()
  }
}
</script>

<style lang="scss" scoped>
body,h1,h2,h3,h4,h5 {font-family: "Raleway", sans-serif}
.topmg{
    margin-top: 100px
}

.mrgntop {
  margin-top: 10px
}

</style>
