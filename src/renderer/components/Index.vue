<template>
  <div class="Index">
    <h3 class="comIndexTitle"><strong>最新视频</strong><span>共<i>{{numNewVideo}}</i>节课</span><a href="javascript:;">更多</a></h3>
    <div class="swiper-container swiperSlide1">
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
    <RecVideo></RecVideo>
    <SoftVideo></SoftVideo>
    <FontUi></FontUi>
    <CourseC4D></CourseC4D>
    <UiDesign></UiDesign>
    <ChoiceVideo></ChoiceVideo>
  </div>
</template>

<script>
  import axios from 'axios'
  import Swiper from 'swiper'
  import RecVideo from './index/RecVideo'
  import ChoiceVideo from './index/ChoiceVideo'
  import SoftVideo from './index/SoftVideo'
  import FontUi from './index/FontUi'
  import UiDesign from './index/UiDesign'
  import CourseC4D from './index/CourseC4D'
  import 'swiper/dist/css/swiper.min.css'
  export default {
    name: 'Index',
    data () {
      return {
        numNewVideo: 0,
        videoSlide: []
      }
    },
    components: {
      Swiper,
      RecVideo,
      ChoiceVideo,
      SoftVideo,
      FontUi,
      CourseC4D,
      UiDesign
    },
    created () {
      var _this = this
      axios.get('/static/json/newVideo.json')
        .then(function (response) {
          _this.videoSlide = response.data.videoSlide
          _this.numNewVideo = response.data.videoSlide.length
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
          _this.mySwiper = new Swiper('.swiperSlide1', {
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
  .comIndexTitle{
    position: relative; color: #fff;
    a{
      position: absolute; right: 0; top: 0; color: #fff;
    }
  }
  .swiper-container {
    width: 100%;
    height: 300px;
    margin: 20px auto;
    .swiper-slide {
      width: 300px;
      text-align: center;
      font-size: 18px;
      background-color: #dddddd;
      .slideImg{ display: block; width: 100%;}
      .slideTitle{ display: block; width: 90%; margin: 0 auto; text-align: left; white-space: nowrap; overflow: hidden; text-overflow: ellipsis;}
      .slideDetail{
        width: 90%;
        margin: 0 auto;
        overflow: hidden;
        span{ float: left;}
        span:last-child{ float: right;}
      }
    }
  }
</style>
