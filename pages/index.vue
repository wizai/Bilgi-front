<template>
  <section class="page-homepage">
    <!-- <header>
      <nuxt-link :to="{ name: 'login' }" class="nav-link">
        Login
      </nuxt-link>
      <nuxt-link :to="{ name: 'register' }" class="nav-link">
        Register
      </nuxt-link>

    </header> -->
    <div>
      <div class="gradientWhite"></div>
      <div class="redBlock"></div>
      <section class="page-listingFilms containerSlider">
        <flickity ref="flickity" :options="flickityOptions" class="sliderListingFilms">
          <div class="carousel-cell" v-for="slide in slides" :key="slide._id">
              <p>{{ slide.letter }}</p>
          </div>
        </flickity>
        <nuxt-link :to="'./article/'+ currentLetter" class="chooseButton">Voir un article</nuxt-link>
      </section>
      <progressbar :sliderCurrent="sliderCurrent" :sliderMax="sliderMax" :progress="progress"></progressbar>
    </div>
  </section>
</template>

<script>

  import progressbar from "~/components/slider/progressBar.vue";

  export default {

    data() {
      return {
        slides: [
          {
            "_id": 1,
            "letter": 'Aa'
          },
          {
            "_id": 2,
            "letter": 'Bb'
          },
          {
            "_id": 3,
            "letter": 'Cc'
          },
          {
            "_id": 4,
            "letter": 'Dd'
          },
          {
            "_id": 5,
            "letter": 'Ee'
          },
          {
            "_id": 6,
            "letter": 'Ff'
          },
          {
            "_id": 7,
            "letter": 'Gg'
          },
          {
            "_id": 8,
            "letter": 'Hh'
          },
          {
            "_id": 9,
            "letter": 'Ii'
          },
          {
            "_id": 10,
            "letter": 'Jj'
          },
          {
            "_id": 11,
            "letter": 'Kk'
          },
          {
            "_id": 12,
            "letter": 'Ll'
          },
          {
            "_id": 13,
            "letter": 'Mm'
          },
          {
            "_id": 14,
            "letter": 'Nn'
          },
          {
            "_id": 15,
            "letter": 'Oo'
          },
          {
            "_id": 16,
            "letter": 'Pp'
          },
          {
            "_id": 17,
            "letter": 'Qq'
          },
          {
            "_id": 18,
            "letter": 'Rr'
          },
          {
            "_id": 19,
            "letter": 'Ss'
          },
          {
            "_id": 20,
            "letter": 'Tt'
          },
          {
            "_id": 21,
            "letter": 'Uu'
          },
          {
            "_id": 22,
            "letter": 'Vv'
          },
          {
            "_id": 23,
            "letter": 'Ww'
          },
          {
            "_id": 24,
            "letter": 'Xx'
          },
          {
            "_id": 25,
            "letter": 'Yy'
          },
          {
            "_id": 26,
            "letter": 'Zz'
          }
        ],
        flickityOptions: {
          contain: true,
          imagesLoaded: true,
          prevNextButtons: false,
          pageDots: false,
          wrapAround: true,
          accessibility: true,
        },

        sliderCurrent: "01",
        sliderMax: "26",
        duration: 6,
        interval: 10,
        percentTime: '',
        step: '',
        tick: '',
        isPaused: false,
        progress: '0',
        currentLetter : 'A'
      }
    },

    beforeDestroy() {
      clearInterval(this.tick);
    },

    methods: {
      logout() {
        this.$auth.logout();
      },

      updateStatus() {
        let flkty = this.$refs.flickity.$flickity;
        this.sliderCurrent = flkty.selectedIndex + 1;
        this.sliderMax = flkty.slides.length;

        if ((flkty.selectedIndex + 1) < 10) {
          this.sliderCurrent = "0" + (flkty.selectedIndex + 1);
        }
        if ((flkty.slides.length) < 10) {
          this.sliderMax = "0" + (flkty.slides.length);
        }
      },

      startProgressbar() {
        const $this = this;
        this.resetProgressbar();
        this.percentTime = 0;
        this.isPaused = false;
        this.tick = setInterval(() => {
          $this.increase();
        }, this.interval);
      },

      increase() {
        if (!this.isPaused) {
          this.step = (this.duration * 1000) / this.interval;
          this.percentTime += 100 / this.step;
          this.progress = this.percentTime + "%";
          if (this.percentTime >= 100) {
            this.$refs.flickity.next();
            this.startProgressbar();
          }
        }
      },

      resetProgressbar() {
        this.progress = 0 + '%';
        clearTimeout(this.tick);
      },

      linkToLetter(){
        let flkty = this.$refs.flickity.$flickity;
        let sliderCurrent = flkty.selectedIndex + 1;
        let letterLink = this.slides.filter(slide => slide._id === sliderCurrent);
        this.currentLetter = letterLink[0].letter[0];
      }

    },

    mounted: function () {

      let flkty = this.$refs.flickity.$flickity;
      let redBlock = document.querySelector('.redBlock');

      flkty.on('change', function (index) {
        redBlock.classList.add("mystyle");
      });

      flkty.on('settle', function (index) {
        redBlock.classList.remove("mystyle");
      });

      let $this = this;
      let sliderContainer = document.querySelector('.containerSlider');

      sliderContainer.addEventListener('mouseenter', function () {
        $this.isPaused = true;
      });
      sliderContainer.addEventListener('mouseleave', function () {
        $this.isPaused = false;
      });

      this.$nextTick(function () {
        this.$refs.flickity.on('change', function () {
          //$this.isPaused = true;
          $this.updateStatus();
          $this.linkToLetter();
        });

        this.startProgressbar();
        this.updateStatus();
        this.linkToLetter();
      });


      // Set the name of the hidden property and the change event for visibility
      let hidden, visibilityChange;
      if (typeof document.hidden !== "undefined") { // Opera 12.10 and Firefox 18 and later support
        hidden = "hidden";
        visibilityChange = "visibilitychange";
      } else if (typeof document.msHidden !== "undefined") {
        hidden = "msHidden";
        visibilityChange = "msvisibilitychange";
      } else if (typeof document.webkitHidden !== "undefined") {
        hidden = "webkitHidden";
        visibilityChange = "webkitvisibilitychange";
      }

      // If the page is hidden, pause the video;
      // if the page is shown, play the video
      function handleVisibilityChange() {
        if (document[hidden]) {
          this.isPaused = true;
        } else {
          this.isPaused = false;
        }
      }

      // Warn if the browser doesn't support addEventListener or the Page Visibility API
      if (typeof document.addEventListener === "undefined" || hidden === undefined) {
        console.log("This demo requires a browser, such as Google Chrome or Firefox, that supports the Page Visibility API.");
      } else {
        // Handle page visibility change
        document.addEventListener(visibilityChange, handleVisibilityChange, false);

      }

    },

    components: {
      progressbar
    },
  }

</script>

<style lang="scss">

  @import "@/assets/scss/style.scss";

  .page-listingFilms {
    position: absolute;
    width: 100%;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
  }

  .sliderListingFilms {
    @include flexbox();
    @include align-items(center);
    @include justify-content(center);

    .flickity-viewport {
      width: 100%;
      @include flexbox();
      @include align-items(center);
      @include justify-content(center);
    }

    .flickity-slider {
      height: 100%;
      @include flexbox();
      @include align-items(center);
      @include justify-content(center);
    }


    .carousel-cell {
      width: 200px;
      height: 200px;
      margin: 0 75px;
      position: relative;
      @include flexbox();
      @include align-items(center);
      @include justify-content(center);

      & p {
        font-size: 80px;
        color: #fff;
        font-weight: bold;

        @media #{$mobile} {
          font-size: 40px;
        }
      }
    }

    &__item {
      width: 100%;
      height: 100%;
      background: 50% no-repeat;
      background-size: cover;
      @include flexbox();
      @include align-items(center);
      @include justify-content(center);
      pointer-events: none;
      cursor: default;

      &--title {
        font-weight: 700;
        font-size: 40px;
        max-width: 600px;
        text-align: center;
        color: #fff;
        text-shadow: 0 2px 4px rgba(0, 0, 0, .5);
      }
    }
  }

  .chooseButton {
    position: absolute;
    top: 100%;
    left: 50%;
    transform: translate(-50%, 20px);
    display: inline-block;
    border-radius: 30px;
    background-color: #fff;
    color: $blue;
    padding: 15px 25px;
    font-family: $Circular;
  }

  .slider-calendarNavbar {
    position: fixed;
    bottom: 0px;
    left: 0;
  }

  .page-homepage {
    background: radial-gradient(#183E80, #001447);
    background-size: cover;
    height: 100vh;
    width: 100%;
    color: #ffffff;
    position: relative;
  }

  .gradientWhite {
    position: absolute;
    width: 500px;
    height: 500px;
    background-color: rgb(13, 42, 102);
    border-radius: 50%;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);

    @media #{$mobile} {
      width: 300px;
      height: 300px;
    }
  }

  .redBlock {
    position: absolute;
    width: 200px;
    height: 200px;
    background-color: rgb(214, 52, 0);
    border-radius: 50%;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    transition: .2s;

    @media #{$mobile} {
      width: 120px;
      height: 120px;
    }
  }

  .redBlock.mystyle {
    width: 0px;
    height: 0px;
  }

</style>
