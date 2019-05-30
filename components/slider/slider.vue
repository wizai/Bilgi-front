<template>

  <section class="page-listingFilms containerSlider">
    <flickity ref="flickity" :options="flickityOptions" class="sliderListingFilms">
      <div class="carousel-cell" v-for="slide in slides" :key="slide._id">
          <p>{{ slide.letter }}</p>
      </div>
    </flickity>
    <a href="">Voir cette lettre</a>
  </section>

</template>

<script>

  export default {
    name: "slider",
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
        }
      }
    },
  }
</script>

<style lang="scss">

  @import "@/assets/scss/style.scss";

  .page-listingFilms{
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

      & p{
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        font-size: 80px;
        color: #fff;
        font-weight: bold;
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

  .slider-calendarNavbar {
    position: fixed;
    bottom: 0px;
    left: 0;
  }


</style>
