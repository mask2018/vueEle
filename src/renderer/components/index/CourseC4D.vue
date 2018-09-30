<template>
  <div class="RecVideo">
    <h3 class="comIndexTitle"><strong>C4D教程</strong><span>共<i>{{numFontVideo}}</i>节课</span><a href="javascript:;">更多</a></h3>
    <div class="fontUicen">
      <div class="fontUiMore">
        <a href="javascript:;">C4D教程</a>
        <a href="javascript:;">查看更多</a>
      </div>
      <div class="swiper-container swiperSlide6">
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
        numFontVideo: 0,
        videoSlide: []
      }
    },
    components: {
      Swiper
    },
    created () {
      var _this = this
      axios.get('/static/json/courseC4D.json')
        .then(function (response) {
          _this.videoSlide = response.data.videoSlide
          _this.numFontVideo = response.data.videoSlide.length
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
          _this.mySwiper = new Swiper('.swiperSlide6', {
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

<style scoped lang="less">
.fontUicen{
  position: relative;
  overflow: hidden;
  .fontUiMore{
    position: absolute; left: 0; top: 0;
    width: 300px; height: 300px; margin-top: 20px; line-height: 150px;
    background-color: #dddddd; text-align: center;
  }
  .swiperSlide6{
    margin-left: 330px;
    .swiper-button-next{
      right: 340px;
    }
  }
}
</style>
