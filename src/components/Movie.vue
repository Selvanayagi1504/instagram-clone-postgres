<template>
  <div class="movie">
    <h2>{{ movie.Title }}</h2>
    <div>
      <img width="200" :alt="altText" :src="movie.Poster" />
    </div>
    <p>{{ movie.Year }}</p>
    <!-- <button @click="add(`${movie.Title}`,`${movie.Poster}`,`${movie.Year}`)">Add to favourites</button> -->
    <button @click="add(`${movie.Title}`,`${movie.Poster}`,`${movie.Year}`)" v-show="!isFavorite">Add to favorites</button>
    <button @click="remove(`${movie.Title}`)" v-show="isFavorite">Delete from favorites</button>
  </div>
</template>

<script>
  import { computed } from '@vue/composition-api';

  export default {
    name: "Movie",
    props: ['movie'],
    data(){
      return{
        movies:[]
      }
    },
    setup({ movie }) {
      
      const altText = computed(() => `The movie titled: ${movie.Title}`);
      var t=false
      let email = sessionStorage.getItem('email');
      fetch("https://secret-ridge-70355.herokuapp.com/api/user/getuser/"+email)
        .then(response => response.json())
        .then(user => {
          let users = JSON.parse(user.fav);
              console.log(users)
          users.forEach(u => {
            console.log(u.title)
            if(movie.Title==u.title){
              t=true
            }
        })
        console.log(t)
      })
       
      return { altText,movies:[],isFavorite:t };
    },
    methods:{
      remove(title){
        this.isFavorite=false
        let users = ""
        this.movies.forEach(m=>{
          if(title!=m.title){
            users.push(m);
          }
        })
        this.movies=users;
        this.saveimage()
      },
    add(title,poster,year) {
      this.isFavorite=true
      var movie = {
          title: title,
          poster: poster,
          year: year
      }
      console.log(movie)
      this.movies.push(movie)
      alert("movie added to favourites")
      this.saveimage();
    },
    saveimage() {
       let email=sessionStorage.getItem('email');
      fetch("https://secret-ridge-70355.herokuapp.com/api/user/changefav/"+email, {   
          method: "POST", 
          body: JSON.stringify(
              this.movies
          ),  
          headers: { 
              "Content-type": "application/json; charset=UTF-8"
          } 
      }) 
      .then(response => response.json()) 
      .then(json => console.log(json));
    }
    }
  };
</script>
