<template>
  <div class="products__item" v-if="info" @click="$router.push(`/product/${330 + number + num}`)">
      <img class="products__item-img" :src="`https://www.themoviedb.org/t/p/w220_and_h330_face/${info.poster_path}`" alt="">
      <div class="products__popularity">
          <div class="products__popularity-inner">{{(info.vote_average * 10 ).toFixed()}}</div>
      </div>
      <div class="products__item-box">
          <h3 class="products__item-title">{{info.original_title}}</h3>
          <p class="products__item-text">{{dateProduct}}</p>
      </div>
  </div>
</template>

<script>
import axios from 'axios'
    export default {
  data () {
    return {
      info: null,
      num: 0
    }
  },
  props:{
    number: {
      type: Number,
      default: 400
    }
  },
  methods: {
    async productMain () {
      await axios
        .get(`https://api.themoviedb.org/3/movie/${330 + this.number + this.num}?api_key=369031ad3b6ef6290aa938594197f235` ,{
            headers: {             
            "Content-Type": "application/json",          
            }
          })
        .then(response => {
          this.info = response.data
          this.num = 0
        })
        .catch(error => {
          console.log(error)
          this.num += 20
          this.productMain()
        })
    }
  },
  computed: {
    dateProduct () {
      let month
      const arr = this.info.release_date.split('-').reverse()
      switch (arr[1]) {
          case "01": month = 'янв'; break;
          case "02": month = 'феб'; break;
          case "03": month = 'мар'; break;
          case "04": month = 'апр'; break;
          case "05": month = 'май'; break;
          case "06": month = 'июн'; break;
          case "07": month = 'июл'; break;
          case "08": month = 'авг'; break;
          case "09": month = 'сен'; break;
          case "10": month = 'окт'; break;
          case "11": month = 'ноя'; break;
          default: month = 'дек';
        }
      return arr[0] + ' ' + month + ' ' + arr[2]
    }
  },
  created () {
    this.productMain()
  }
}
</script>

<style scoped>
.products__item-img{
    width: 100%;
    height: 225px;
    border-radius: 10px;
}
.products__popularity{ 
    position: relative;
}
.products__popularity-inner{
    width: 34px;
    height: 34px;
    border-radius: 50% 50%;
    background-color: #000;
    padding-right: 5px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 0.6em;
    color: #fff;
    border: 2px solid yellowgreen;
    position: absolute;
    left: 10px;
    top: -15px;
}
.products__popularity::before{
    content: '%';
    position: absolute;
    font-size: 8px;
    color: #fff;
    left: 32px;
    top: -10px;
    z-index: 1;
}
.products__item-box{
    width: 100%;
    padding: 26px 10px 12px 10px;
}
.products__item-title{
    font-weight: 700;
    color: #000;
    font-size: 14px;
    margin: 0;
}
.products__item-text{
    font-size: 14px;
    margin: 5px 0 0 0;
    padding: 0;
    color: rgba(0,0,0,0.6);
}
 
</style>