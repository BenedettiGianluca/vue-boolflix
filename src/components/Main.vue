<template>
  <main class="main">
    <input type="text" placeholder="Digita il nome di un film o di una serie tv" v-on:keyup.enter="ricerca">
    <div class="filmSerieTrovati">
      <div class="film" v-for="(element, filmsIndex) in films" :key="filmsIndex" @mouseover="mockupFilmOver" @mouseleave="mockupFilmLeave">
        <img class="poster" :src="`https://image.tmdb.org/t/p/w342${element.poster_path}`">
        <div class="info">
          <h2>Titolo: {{element.title}}</h2>
          <h3>Titolo originale: {{element.original_title}}</h3>
          <p>Lingua: <span v-if="((element.original_language!='it')&&(element.original_language!='en')&&(element.original_language!='fr'))">non specificata</span>
            <img v-if="(element.original_language=='it')" src="https://7laghikartitalia.it/wp-content/uploads/Bandiera-d-Italia-1920x1080.jpg">
            <img v-if="(element.original_language=='en')" src="https://besthqwallpapers.com/Uploads/26-5-2019/94067/thumb2-flag-of-united-kingdom-4k-stone-background-grunge-flag-europe.jpg">
            <img v-if="(element.original_language=='fr')" src="https://p4.wallpaperbetter.com/wallpaper/824/310/435/flags-flag-of-france-wallpaper-preview.jpg">
          </p>
          <p>Voti: {{element.vote_count}}</p>
          <p class="stelle">Valutazione: 
            <i v-if="Math.ceil(element.vote_average/2)>=1" class="fas fa-star"></i>
            <i v-if="Math.ceil(element.vote_average/2)>=2" class="fas fa-star"></i>
            <i v-if="Math.ceil(element.vote_average/2)>=3" class="fas fa-star"></i>
            <i v-if="Math.ceil(element.vote_average/2)>=4" class="fas fa-star"></i>
            <i v-if="Math.ceil(element.vote_average/2)>=5" class="fas fa-star"></i>
          </p>
          <p>Trama: {{element.overview}}</p>
        </div>
      </div>
      <div class="tvShow" v-for="(element, seriesIndex) in series" :key="seriesIndex" @mouseover="mockupTvShowOver" @mouseleave="mockupTvShowLeave">
        <img class="poster" :src="`https://image.tmdb.org/t/p/w342${element.poster_path}`">
        <div class="info">
          <h2>Titolo: {{element.name}}</h2>
          <h3>Titolo originale: {{element.original_name}}</h3>
          <p>Lingua: <span v-if="((element.original_language!='it')&&(element.original_language!='en')&&(element.original_language!='fr'))">non specificata</span>
            <img v-if="(element.original_language=='it')" src="https://7laghikartitalia.it/wp-content/uploads/Bandiera-d-Italia-1920x1080.jpg">
            <img v-if="(element.original_language=='en')" src="https://besthqwallpapers.com/Uploads/26-5-2019/94067/thumb2-flag-of-united-kingdom-4k-stone-background-grunge-flag-europe.jpg">
            <img v-if="(element.original_language=='fr')" src="https://p4.wallpaperbetter.com/wallpaper/824/310/435/flags-flag-of-france-wallpaper-preview.jpg">
          </p>
          <p>Voti: {{element.vote_count}}</p>
          <p class="stelle">Valutazione: 
            <i v-if="Math.ceil(element.vote_average/2)>=1" class="fas fa-star"></i>
            <i v-if="Math.ceil(element.vote_average/2)>=2" class="fas fa-star"></i>
            <i v-if="Math.ceil(element.vote_average/2)>=3" class="fas fa-star"></i>
            <i v-if="Math.ceil(element.vote_average/2)>=4" class="fas fa-star"></i>
            <i v-if="Math.ceil(element.vote_average/2)>=5" class="fas fa-star"></i>
          </p>
          <p>Trama: {{element.overview}}</p>
        </div>
      </div>
    </div>
  </main>
</template>

<script>
  import axios from 'axios';

  export default {
    name: 'Main',
    data(){
      return {
        apiMoviesURL: 'https://api.themoviedb.org/3/search/movie',
        apiSeriesURL: 'https://api.themoviedb.org/3/search/tv',
        films: [],
        series: []
      }
    },
    methods: {
      ricerca: function(){
        let filtroRicerca = document.querySelector('.main>input').value;
        axios
        .get(this.apiMoviesURL, {
          params: {
            api_key: '35c708968a77a980b6cd9af13310e62e',
            query: filtroRicerca,
          },
        })
        .then(risposta => {
          this.films = risposta.data.results;
        })
        .catch(function (error) {
          console.log(error);
        });
  
        axios
        .get(this.apiSeriesURL, {
          params: {
            api_key: '35c708968a77a980b6cd9af13310e62e',
            query: filtroRicerca,
          },
        })
        .then(risposta => {
          this.series = risposta.data.results;
        })
        .catch(function (error) {
          console.log(error);
        });
      },

      mockupFilmOver: function(){
        let mark = event.target;
        let markClass = event.target.getAttribute('class');
        if(markClass=="film"){
          let info = mark.querySelector('.info');
          let mockup = mark.querySelector('.poster');
          console.log(info);
          console.log(mockup);
          info.style.display = "block";
          mockup.style.display = "none";
        }
        if(markClass!="film"){
          let info = mark.parentNode.querySelector('.info');
          let mockup = mark.parentNode.querySelector('.poster');
          console.log(info);
          console.log(mockup);
          info.style.display = "block";
          mockup.style.display = "none";
        }
      },

      mockupFilmLeave: function(){
        let mark = event.target;
        let markClass = event.target.getAttribute('class');
        if(markClass=="film"){
          let info = mark.querySelector('.info');
          let mockup = mark.querySelector('.poster');
          console.log(info);
          console.log(mockup);
          info.style.display = "none";
          mockup.style.display = "block";
        }
        if(markClass!="film"){
          let info = mark.parentNode.querySelector('.info');
          let mockup = mark.parentNode.querySelector('.poster');
          console.log(info);
          console.log(mockup);
          info.style.display = "none";
          mockup.style.display = "block";
        }
      },

      mockupTvShowOver: function(){
        let mark = event.target;
        let markClass = event.target.getAttribute('class');
        if(markClass=="tvShow"){
          let info = mark.querySelector('.info');
          let mockup = mark.querySelector('.poster');
          console.log(info);
          console.log(mockup);
          info.style.display = "block";
          mockup.style.display = "none";
        }
        if(markClass!="tvShow"){
          let info = mark.parentNode.querySelector('.info');
          let mockup = mark.parentNode.querySelector('.poster');
          console.log(info);
          console.log(mockup);
          info.style.display = "block";
          mockup.style.display = "none";
        }
      },

      mockupTvShowLeave: function(){
        let mark = event.target;
        let markClass = event.target.getAttribute('class');
        if(markClass=="tvShow"){
          let info = mark.querySelector('.info');
          let mockup = mark.querySelector('.poster');
          console.log(info);
          console.log(mockup);
          info.style.display = "none";
          mockup.style.display = "block";
        }
        if(markClass!="tvShow"){
          let info = mark.parentNode.querySelector('.info');
          let mockup = mark.parentNode.querySelector('.poster');
          console.log(info);
          console.log(mockup);
          info.style.display = "none";
          mockup.style.display = "block";
        }
      }
    }
  }
</script>

<style lang="scss">
  .main {

    input {
      background-color: #500800;
      color: #33C933;
      height: 25px;
      width: 60vw;
      margin: 6vh 30px 5vh 200px;

      &::placeholder {
        color: #219621;
        opacity: 1;
      }
      &:-ms-input-placeholder {
        color: #219621;
      }
      &::-ms-input-placeholder {
        color: #219621;
      }
    }

    .filmSerieTrovati {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      align-items: flex-start;
      height: 60vh;
      padding: 30px;
      margin: 0 50px;

      .film, .tvShow {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        height: 450px;
        border: 1px solid grey;
        margin: 30px;

        .poster {
          height: 100%;
        }

        .info {
          display: none;
          height: 100%;
          width: 342px;
          padding: 30px;
          overflow: scroll;
          &::-webkit-scrollbar {
            display: none;
          }

          h2, h3, p {
            color: #ffffee;
            padding: 10px 0;
  
            img {
              height: 18px;
              width: 24px;
            }
  
            .fa-star {
              color: yellow;
            }
          }
        }        
      }
    }
  }
</style>