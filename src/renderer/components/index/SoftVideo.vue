<template>
  <div class="RecVideo">
    <h3 class="comIndexTitle"><strong>软件入门</strong><a href="javascript:;">更多</a></h3>
    <div class="swiper-container swiperSlide4">
      <div class="swiper-wrapper">
        <div class="swiper-slide" v-for="(data, index) in videoSlide" v-bind:class="'sortlist'+index" :key='data.id'>
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
      axios.get('/static/json/softVideo.json')
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
          _this.mySwiper = new Swiper('.swiperSlide4', {
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

<style scoped>
.swiperSlide4 .sortlist0:after{
  content: '1';
  position: absolute; top: 0; left: 0; display: block;
  width: 60px; height: 60px; line-height: 60px; text-align: center;
  background-color: bisque;
}
.swiperSlide4 .sortlist1:after{
  content: '2';
  position: absolute; top: 0; left: 0; display: block;
  width: 60px; height: 60px; line-height: 60px; text-align: center;
  background-color: bisque;
}
.swiperSlide4 .sortlist2:after{
  content: '3';
  position: absolute; top: 0; left: 0; display: block;
  width: 60px; height: 60px; line-height: 60px; text-align: center;
  background-color: bisque;
}
</style>
