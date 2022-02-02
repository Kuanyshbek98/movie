<template>
  <div class="home">
    <div class="home__block">
      <h1 class="home__title">Что популярно</h1>
      <ul class="home__list">
        <li class="home__item" v-for="(item,index) in productNumber" :key="index">
          <ProductsBlock :number="index"/>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default{
  data () {
    return {
      productNumber: 10
    }
  },
  components: {
    ProductsBlock: () => ({
      component: import('@/components/products')
    })
  },
  mounted () {
      const link = document.querySelector(".home__list");
      link.addEventListener("scroll", (event) => {
        if (event.target.scrollLeft > 270) {
          this.productNumber = 20
        }
      });
  }
}
</script>

<style>
.home__block{
  width: 90%;
  margin: 5% auto 5%;
  background-color: #fff;
  padding-top: 20px;
}
.home__title{
  margin: 0;
  padding-left: 40px;
  font-size: 1.5em;
  font-weight: 600;
}
.home__list{
  padding: 20px 20px 20px 0;
  display: flex;
  overflow-x: auto;
}
.home__item{
  min-width: 150px;
  height: auto;
  margin-left: 40px;
  cursor: pointer;
  list-style: none;
}
</style>