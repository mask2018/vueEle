<template>
  <div class="RecVideo">
    <h3 class="comIndexTitle"><strong>精选专辑</strong><a href="javascript:;">更多</a></h3>
    <div class="swiper-container swiperSlide3">
      <div class="swiper-wrapper">
        <div class="swiper-slide" v-for="data in videoSlide" :key='data.id'>
          <a :href="data.method" class="slideImg"><img v-bind:src="data.src"/></a>
          <a :href="data.method" class="slideTitle">{{data.title}}</a>
          <p class="slideDetail"><span>{{data.label}}</span><span><i>{{data.number}}</i>人已学</span></p>
        </div>
      </div>
      <div class="swiper-button-next"></div>
      <div class="swiper-button-prev"></div>
    </div>
  </div>
</template>

<script>
  import axios from 'axios'
  import Swiper from 'swiper'
  import 'swiper/dist/css/swiper.min.css'
  export default {
    name: 'Index',
    data () {
      return {
        videoSlide: []
      }
    },
    components: {
      Swiper
    },
    created () {
      var _this = this
      axios.get('/static/json/choiceVideo.json')
        .then(function (response) {
          _this.videoSlide = response.data.videoSlide
          _this.recSlide()
        }).catch(function (error) {
          console.log(error)
        })
    },
    mounted () {
    },
    methods: {
      recSlide: function () {
        var _this = this
        _this.$nextTick(function () {
          _this.mySwiper = new Swiper('.swiperSlide3', {
            loop: true,
            slidesPerView: 'auto',
            spaceBetween: 30,
            prevButton: '.swiper-button-prev',
            nextButton: '.swiper-button-next',
            observer: true
          })
        })
      }
    }
  }
</script>

<style lang="less">
</style>
