<template>
  <div class="home">
    <div class="swiper">
      <!-- 底層Swipper -->
      <swiper ref="mySwiper" :options="swiperOptions" class="swiper-container">
        <swiper-slide class="slide"><img src="@/assets/image/bg1.jpeg" alt="" class="bg"></swiper-slide>
        <swiper-slide class="slide"><img src="@/assets/image/bg2.jpeg" alt="" class="bg"></swiper-slide>
        <swiper-slide class="slide"><img src="@/assets/image/bg3.jpeg" alt="" class="bg"></swiper-slide>
        <swiper-slide class="slide"><img src="@/assets/image/bg4.jpeg" alt="" class="bg"></swiper-slide>
        <div class="swiper-pagination" slot="pagination"></div>
      </swiper>
      <!-- 黑色遮罩 -->
      <div class="blackbg">
        <div class="blackbg-inside"></div>
      </div>

      <div class="container">
       <div class="container-inside">
          <!-- left container -->
          <div class="left-container">
            <div class="logo">
              <img src="@/assets/image/logo.svg" alt="">
            </div>
            <div class="title-text">
              <p class="font font-h5 font-light">好室旅店。HOUSE HOTEL</p>
              <p class="font-h5 font-light">花蓮縣花蓮市國聯一路1號</p>
              <p class="font-h5 font-light">03-8321155</p>
              <p class="font-h5 font-light">HOUSE@HOTEL.COM</p>
            </div>
          </div>

          <div class="grid-button">
            <div><img src="@/assets/image/room1A.jpeg" alt="" class="room"></div>
            <div><img src="@/assets/image/room2A.jpeg" alt="" class="room"></div>
            <div><img src="@/assets/image/room3A.jpeg" alt="" class="room"></div>
            <div><img src="@/assets/image/room4A.jpeg" alt="" class="room"></div>
            <div><img src="@/assets/image/room5A.jpeg" alt="" class="room"></div>
            <div><img src="@/assets/image/room6A.jpeg" alt="" class="room"></div>
          </div>
       </div>
      </div>
      
      
    </div>
  
  </div>
</template>

<script> 
// import { Carousel, Slide } from 'vue-carousel'
// import $ from 'jquery'
import { Swiper, SwiperSlide, directive } from 'vue-awesome-swiper'
import 'swiper/swiper-bundle.css'

export default {
  components: { Swiper, SwiperSlide },
  directives: {
    swiper: directive
  },
  data (){
    return {
      swiperOptions: {
        // spaceBetween: 30,
        pagination: {
          el: '.swiper-pagination',
          clickable: true
        },
      },
      imgList:[
        {
          name: "@/assets/image/bg1.jpeg"
        },
        {
          name: "@/assets/image/bg2.jpeg"
        },
        {
          name: "@/assets/image/bg3.jpeg"
        },
        {
          name: "@/assets/image/bg4.jpeg"
        }
      ]
    }
  },
  computed: {
    swiper () {
      return this.$refs.mySwiper.$swiper
    }
  },
  mounted () {
    console.log('Current Swiper instance object', this.swiper)
    // this.swiper.slideTo(3, 20000, true)
  }
}
</script>
