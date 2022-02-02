<template>
    <div v-if="info" class="film-block" :style="`background-image: url(https://www.themoviedb.org/t/p/w220_and_h330_face/${info.backdrop_path});`">
        <div class="film-block__wrap">
            <img class="film-block__img" :src="`https://www.themoviedb.org/t/p/w220_and_h330_face/${info.poster_path}`" alt="">
            <div class="film-block__info">
                <h1 class="film-block__name">{{info.original_title}} ({{info.release_date.split('-')[0]}})</h1>
                <label v-for="(item,index) in info.genres" :key="index" class="film-block__text">{{item.name}} ,</label>
                    <ul class="film-block__reating-items">
                        <li class="film-block__reating-item">
                            <div class="news__popularity-inner">{{(info.vote_average * 10 ).toFixed()}}
                            </div>
                            <p class="film-block__reating-text">Пользовательский счёт</p>
                        </li>
                        <li class="film-block__reating-item">
                            <span class="film-block__reating-span">+</span>
                        </li>
                        <li class="film-block__reating-item">
                            <span class="film-block__reating-span">+</span>
                        </li>
                        <li class="film-block__reating-item">
                            <span class="film-block__reating-span">+</span>
                        </li>
                        <li class="film-block__reating-item">
                            <span class="film-block__reating-span">+</span>
                        </li>
                    </ul>
                    <strong class="film-block__strong">{{info.title}}</strong>
                <h2 class="film-block__title">Обзор</h2>
                <p class="film-block__text">{{info.overview}}</p>
                
                <h3 v-if="info.creator" class="film-block__title">James Gunn</h3>
                <p v-if="info.creator" class="film-block__text">Создатель</p>
            </div>
        </div>
        <div class="bg"></div>
    </div>
</template>

<script>
import axios from 'axios'
    export default {
  data () {
    return {
      info: null,
      data: 0
    }
  },
  methods: {
    async productMain () {
      await axios
        .get(`https://api.themoviedb.org/3/movie/${this.$route.params.id}?api_key=369031ad3b6ef6290aa938594197f235` ,{
            headers: {             
            "Content-Type": "application/json",          
            }
          })
        .then(response => {
          this.info = response.data
          console.log(this.info)
          this.data = 0
        })
        .catch(error => {
          console.log(error)
          this.data += 20
          this.productMain()
        })
        .finally(() => (this.load = false))
    }
  },
  created () {
    this.productMain()
  }
}
</script>

<style scoped>
.film-block{
    height: 510px;
    margin: 50px 0px;
    background-size: 100%;
    background-repeat: no-repeat;
    background-position: center center;
    background-size: cover;
    color: #fff;
    position: relative;
    box-sizing: border-box;
}
.bg{
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    z-index: 1;
    background-color: #000000bb;
}
.film-block__wrap{
    padding: 50px;
    display: flex;
    align-items: center;
    position: absolute;
    top: 0;
    left: 0;
    width: 90%;
    height: 100%;
    z-index: 2;
}
.film-block__img{
    height: 100%;
    border-radius: 15px;
}
.film-block__reating{
    height: 68px;
    border: 1px solid;
    margin: 20px 0;
    display: flex;
}
.news__popularity-inner{
    width: 69px;
    height: 68px;
    border-radius: 50% 50%;
    background-color: #132614;
    padding-right: 10px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 1.3em;
    color: #fff;
    border: 5px solid yellowgreen;
    position: relative;
}
.news__popularity-inner::before{
    content: '%';
    position: absolute;
    font-size: 12px;
    color: #fff;
    left: 34px;
    top: 6px;
    z-index: 1;
}
.film-block__reating-text{
    margin: 0 0 0 6px;
    width: 140px;
}
.film-block__reating-items{
    display: flex;
    align-items: center;
    padding: 0;
}
.film-block__reating-item{
    margin: 20px 0;
    list-style: none;
    display: flex;
    align-items: center;
    justify-content: space-between;
}
.film-block__reating-item:not(:last-child){
  margin-right: 20px;  
}
.film-block__reating-span{
    width: 46px;
    height: 46px;
    border-radius: 50% 50%;
    background-color: #032541;
    color: #fff;
    display: flex;
    align-items: center;
    justify-content: center;
}
.film-block__info{
    margin-left: 40px;
}
.film-block__strong{
    color: #fff;
    margin-bottom: 0;
    font-size: 1.1em;
    font-weight: 400;
    font-style: italic;
    opacity: 0.7;
}
.film-block__name, .film-block__text{
    margin: 0;
}
.film-block__title{
    font-size: 22px;
    margin: 18px 0 5px 0;
}
.film-block__text{
    font-size: 16px;
}
</style>