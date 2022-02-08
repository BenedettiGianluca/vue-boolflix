<template>
  <main class="main">
    <div class="filmSerieTrovati">
      <div class="film" v-for="(element, filmsIndex) in films" :key="`film${filmsIndex}`" @mouseover="mockupFilmOver" @mouseleave="mockupFilmLeave" :style="`background-image: url('https://image.tmdb.org/t/p/w342/${element.poster_path}');`">
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
      <div class="tvShow" v-for="(element, seriesIndex) in series" :key="`tvShow${seriesIndex}`" @mouseover="mockupTvShowOver" @mouseleave="mockupTvShowLeave" :style="`background-image: url('https://image.tmdb.org/t/p/w342/${element.poster_path}');`">
        <div class="info">
          <h2>Titolo: {{element.name}}</h2>
          <h3>Titolo originale: {{element.original_name}}</h3>
          <p>Lingua: <span v-if="((element.original_language!='it')&&(element.original_language!='en')&&(element.original_language!='fr'))">non specificata</span>
            <img v-if="(element.original_language=='it')" src="https://7laghikartitalia.it/wp-content/uploads/Bandiera-d-Italia-1920x1080.jpg">
            <img v-else-if="(element.original_language=='en')" src="https://besthqwallpapers.com/Uploads/26-5-2019/94067/thumb2-flag-of-united-kingdom-4k-stone-background-grunge-flag-europe.jpg">
            <img v-else-if="(element.original_language=='fr')" src="https://p4.wallpaperbetter.com/wallpaper/824/310/435/flags-flag-of-france-wallpaper-preview.jpg">
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
  export default {
    name: 'Main',
    props: {
      films: Array,
      series: Array
    },
    methods: {
      mockupFilmOver: function(){
        let markClass = event.target.getAttribute('class');
        let info = '';
        if(markClass=="film"){
          info = event.target.querySelector('.info');
        }
        if(markClass!="film"){
          info = event.target.parentNode.querySelector('.info');
        }
        info.style.display = "block";
      },
  
      mockupFilmLeave: function(){
        let markClass = event.target.getAttribute('class');
        let info = '';
        if(markClass=="film"){
          info = event.target.querySelector('.info');
        }
        if(markClass!="film"){
          info = event.target.parentNode.querySelector('.info');
        }
        info.style.display = "none";
      },
  
      mockupTvShowOver: function(){
        let markClass = event.target.getAttribute('class');
        let info = '';
        if(markClass=="tvShow"){
          info = event.target.querySelector('.info');
        }
        if(markClass!="tvShow"){
          info = event.target.parentNode.querySelector('.info');
        }
        info.style.display = "block";
      },
  
      mockupTvShowLeave: function(){
        let markClass = event.target.getAttribute('class');
        let info = '';
        if(markClass=="tvShow"){
          info = event.target.querySelector('.info');
        }
        if(markClass!="tvShow"){
          info = event.target.parentNode.querySelector('.info');
        }
        info.style.display = "none";
      }
    }
  }
</script>

<style lang="scss">
  .main {

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
        width: 342px;
        border: 2px solid grey;
        margin: 30px;

        .info {
          display: none;
          height: 100%;
          width: 340px;
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