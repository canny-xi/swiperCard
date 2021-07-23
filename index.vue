<template>
  <div id="certify">
    <div class="swiper-container">
      <div class="swiper-wrapper">
        <div class="swiper-slide"><img src="../../../../assets/img/a123.png" />
        </div>
        <div class="swiper-slide"><img src="../../../../assets/img/a123.png" />
        </div>
        <div class="swiper-slide"><img src="../../../../assets/img/a123.png" />
        </div>
        <div class="swiper-slide"><img src="../../../../assets/img/a123.png" />
        </div>
        <div class="swiper-slide"><img src="../../../../assets/img/a123.png" />
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import Swiper from 'swiper'
import 'swiper/dist/css/swiper.css'
export default {
  data() {
    return {}
  },
  mounted() {
    this.swiper()
  },
  methods: {
    swiper() {
      let certifySwiper = new Swiper('#certify .swiper-container', {
        watchSlidesProgress: true,
        slidesPerView: 'auto',
        centeredSlides: true,
        loop: true,
        // loopedSlides: 5,
        autoplay: true,
        on: {
          progress: function (progress) {
            for (let i = 0; i < this.slides.length; i++) {
              var slide = this.slides.eq(i)
              var slideProgress = this.slides[i].progress
              let modify = 1
              if (Math.abs(slideProgress) > 1) {
                modify = (Math.abs(slideProgress) - 1) * 0.3 + 1
              }
              let translate = slideProgress * modify * 260 + 'em'
              let scale = 1 - Math.abs(slideProgress) / 5
              let zIndex = 999 - Math.abs(Math.round(10 * slideProgress))
              slide.transform(
                'translateX(' + translate + ') scale(' + scale + ')'
              )
              slide.css('zIndex', zIndex)
              slide.css('opacity', 1)
              if (Math.abs(slideProgress) > 3) {
                slide.css('opacity', 0)
              }
            }
          },
          setTransition: function (transition) {
            for (var i = 0; i < this.slides.length; i++) {
              var slide = this.slides.eq(i)
              slide.transition(transition)
            }
          },
        },
      })
    },
  },
}
</script>
<style lang="less" scoped>
#certify {
  position: absolute;
  top: 55%;
  transform: translate(0, -50%);
  width: 100%;
}

#certify .swiper-container {
  width: 100%;
}

#certify .swiper-slide {
  width: 452px;
  height: 560px;
}

#certify .swiper-slide img {
  display: block;
  width: 100%;
}
</style>