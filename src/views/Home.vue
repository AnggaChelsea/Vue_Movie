<template>
  <div class="home">
   <div class="feature-card">
     <router-link to="/movie/tt3896198" >
     <img src="https://images.alphacoders.com/821/thumb-1920-821092.png" alt="naruto" class="featture-img">
     <div class="detail">
       <h3>Naruto</h3>
       <p>Lorem ipsum dolor sit amet consectetur, adipisicing elit. Error architecto voluptate magni repellendus dolorum accusamus illum aliquid saepe rem sunt itaque nesciunt placeat eos tempore necessitatibus repudiandae rerum, quas explicabo?</p>
     </div>
     </router-link>
   </div>
   <form @submit.prevent="SearchMovies()" class="search-box">
     <input type="text" placeholder="What are you looking for movie"  v-model="search" />
     <input type="submit" value="search " />
   </form>
   <div class="movie-list">
     <div class="movie" v-for="movie in movies" :key="movie.imdbId"> 
       <router-link :to="'/movie/' + movie.imdbId" class="movie-link" >
       <div class="product-images">
         <img :src="movie.Poster" alt="Movie Poster" />
         <div class="type">{{movie.Type}}</div>
         <div class="detail">
           {{movie.Year}}
         </div>
       </div>
       </router-link>
     </div>
   </div>
   </div>
</template>

<script>
import  { ref } from 'vue';
import env from '@/env.js'
export default {
setup(){
  const search = ref('')
  const movies = ref([])

  const SearchMovies = () => {
    if(search.value != ''){
      fetch(`http://www.omdbapi.com/?apikey=${env.apikey}&s=${search.value}`)
      .then(response => response.json())
      .then(data=>{
        movies.value = data.Search;
        search.value = '';
        console.log(movies.value);
      })
    }
  }
  
  return{
    search,
    movies,
    SearchMovies
  }
}
}
</script>

<style lang="scss">
.movie-list {
  display: flex;
  flex-wrap: wrap;
  margin: 0pc 8px;

  .movie{
    max-width: 50%;
    flex: 1 1 50%;

    .movie-link{
      display: flex;
      flex-direction: column;
      height: 100%;

      .product-images{
        position: relative;
        display: block;
        margin: 10px;
        
        .type{
          position: absolute;
          padding:8px 16px;
          background-color:green;
          color: white;
          bottom:86px;
          left:0;
          transition:  capitalize;
        }
        .detail{
          position: absolute;
          padding:8px 16px;
          background-color:green;
          color: white;
          bottom:16px;
          float: right;
          left:0;
          transition:  capitalize;
        }
      }
      img{
          display: block;
          width: 100%;
          height: 300;
          object-fit: cover;
          box-shadow:10px 10px 10px black;
          border-radius:5px;
        }
    }
  }
}
.home{
  .feature-card{
    position:relative;
    .feature-img{
      display: block;
      width: 100%;
      height: 300px;
      object-fit: cover;
      position: relative;
      x-index: 0;
    }
    img{
       display: block;
      width: 100%;
      height: 300px;
      object-fit: cover;
      position: relative;
      x-index: 0;
    }
    .detail{
      position: absolute;
      left: 0;
      right: 0;
      bottom: 0;
      background-color: rgba(0, 0, 0, 0.418);
      padding: 16px;
      z-index: 1;
      h3{
        color: white;
        margin-bottom:16px;
      }
    }
  }

  .search-box{
    margin-top:10px;
    display: flex;
    flex-direction: column;
    margin: 10px;
  }
  input[type="text"]{
    height:40px;
    border: none;
    text-align: center;
    background: rgba(121, 219, 9, 0.534);
    border-radius:10px;
    color: black;

    &::placeholder{
      color: black;
    }
  }
  input[type="submit"]{
    height:30px;
    background: rgba(0, 0, 0, 0.644);
    border-radius:5px;
    margin-top:10px;
    color:green;
  }
}
</style>