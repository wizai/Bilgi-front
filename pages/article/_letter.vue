<template>
  <div v-if="!article.vote_count">
    <section class="news">
      <div class="like"></div>
      <div class="news__container">
        <h1>{{ article.title }}</h1>
        <h2>{{ article.publishedAt }} - {{ article.source.name }}</h2>
        <figure>
          <img :src=" article.urlToImage" :alt=" article.title ">
        </figure>
        <p>
          {{ article.content }}
        </p>
        <div class="buttonContainer">
          <a :href="article.url" class="button" target="_blank">
        <span class="button__text">
          <span class="button_text--src">Voir l'article original</span>
          <svg class="arrow">
            <polygon points="2,2 8,5.5 2,10"></polygon>
          </svg>
        </span>
            <span class="button__circle">
          <span class="button__circle--block"></span>
        </span>
          </a>
        </div>
      </div>
    </section>
  </div>
  <div v-else>
    <section class="movie">
      <div class="movie__title" :style="{ backgroundImage: 'url(http://image.tmdb.org/t/p/original/' + article.backdrop_path + ')'}">
        <h1>{{article.title}}</h1>
      </div>
      <div class="movie__description">
        <div class="movie__description--part1">
          <div class="left">
            <div class="movie__description--part1--affiche">
              <img :src="'http://image.tmdb.org/t/p/w342/' +  `${article.poster_path}`" :alt=" article.title ">
            </div>
            <div class="movie__description--info">
              <span>Date de sortie</span>
              <p>{{ article.release_date}}</p>
            </div>
            <div class="movie__description--info">
              <span>Genre</span>
              <p v-for="genre in article.genres" :key="genre.id">{{ genre.name }}</p>
            </div>
            <div class="movie__description--info">
              <span>Note </span>
              <p>{{ article.popularity }}</p>
            </div>
          </div>
          <div class="right">
            <h2>{{article.title}}</h2>
            <p class="movie__description--part1--synopsis">{{ article.overview }}</p>
          </div>
        </div>
      </div>

    </section>
  </div>
</template>
<script>

  import axios from "axios";

  export default {

    name: "letter",

    data() {
      return {
        article: {}
      }
    },

    mounted: function (){
      var like = document.querySelector('.like');
      like.onclick = function(){
        like.classList.toggle("liked");
      }
    },

    async asyncData({params}) {
      let response = await axios.get('http://127.0.0.1:8000/api/letter/' + params.letter)
      return {
        article: response.data
      }
    },


  }
</script>


<style lang="scss">

  @import "@/assets/scss/style.scss";

  .news {
    position: relative;

    & .like{
      cursor: pointer;
      display: block;
      width: 50px;
      height: 50px;
      position: fixed;
      top: 50%;
      left: 0;
      transform: translate(20px, -50%);
      background: url(../../assets/img/like.svg);
      background-repeat: no-repeat;
      background-size: cover;
      background-position: center center;

      &.liked{
      background: url(../../assets/img/likeOk.svg);
      background-repeat: no-repeat;
      background-size: cover;
      background-position: center center;
      }


      @media #{$mobile} {
        top: inherit;
        left: inherit;
        bottom: 0;
        right: 0;
        transform: translate(-50px, -50px);
      }
    }

    &__container {
      max-width: 900px;
      margin: 0 auto 100px;
      padding: 100px 15px 15px 15px;
      @media #{$mobile} {
        margin: 0 auto 60px;
      }

      & h1 {
        font-weight: bold;
        text-align: center;
        font-size: 40px;
        margin-bottom: 20px;
        @media #{$mobile} {
          font-size: 30px;
          margin-bottom: 20px;
        }
      }

      & h2 {
        text-align: center;
        margin-bottom: 80px;
        font-size: 25px;
        color: $grey;
        font-weight: 500;
        @media #{$mobile} {
          font-size: 18px;
          margin-bottom: 60px;
        }
      }

      & figure {
        width: 100%;
        margin-bottom: 100px;
        @media #{$mobile} {
          margin-bottom: 60px;
        }

        & img {
          display: block;
          width: 100%;
        }
      }

      & p {
        font-size: 18px;
        line-height: 40px;
        font-family: $Georgia;
        @media #{$mobile} {
          font-size: 16px;
          line-height: 35px;
        }
      }

      .buttonContainer {
        text-align: center;
        margin: 100px auto 0;
        @media #{$mobile} {
          margin: 60px auto 0;
        }
      }

      .button {
        text-decoration: none;
        color: $black;
        position: relative;
        display: inline-block;
        font-weight: 700;

        &:hover {

          .button__text:before {
            @include transform(scaleX(0))
          }

          .button__text:after {
            @include transform(scaleX(1));
            transition-delay: .1s;
          }

          .button__circle {
            @include transform(translate(130%, -50%));
            @include transition(all .5s cubic-bezier(.54, .1, 0, .99));
          }

          .arrow {
            @include transform(scaleX(1));
            transition-delay: .25s;
          }

        }

        &__text {
          position: relative;

          &:before, &:after {
            content: "";
            position: absolute;
            top: 50%;
            display: inline-block;
            width: 16px;
            height: 2px;
            background-color: $black;
          }

          &:before {
            right: calc(100% + 6px);
            -webkit-transform-origin: right;
            transform-origin: right;
            @include transition(all .5s cubic-bezier(.54, .1, 0, .99));
          }

          &:after {
            left: calc(100% + 6px);
            -webkit-transform-origin: left;
            transform-origin: left;
            @include transform(scaleX(0));
            @include transition(all .5s cubic-bezier(.54, .1, 0, .99));
          }
        }

        .arrow {
          width: 16px;
          height: 16px;
          position: absolute;
          top: calc(50% - 5px);
          right: -36px;
          -webkit-transform-origin: left;
          transform-origin: left;
          @include transform(scaleX(0));
          @include transition(all .4s cubic-bezier(.54, .1, 0, .99));
          -webkit-transition-delay: 0s;
          transition-delay: 0s;
        }

        &__circle {
          height: 60px;
          position: absolute;
          top: 50%;
          left: -45px;
          right: 0;
          z-index: -1;
          width: 100%;
          @include transform(translateY(-50%));
          @include flexbox();
          -webkit-user-select: none;
          -moz-user-select: none;
          -ms-user-select: none;
          user-select: none;
          pointer-events: none;
          @include transition(all .7s cubic-bezier(.54, .1, 0, .99));

          &--block {
            width: 60px;
            height: 60px;
            -webkit-border-radius: 100%;
            -moz-border-radius: 100%;
            border-radius: 100%;
            @include transition(all .7s cubic-bezier(.54, .1, 0, .99));
            background-color: #eaeaea;
            @include transform(matrix(1, 0, 0, 1, 0, 0));
          }
        }
      }

      @media screen and(max-width: 1070px){
        max-width: 590px;
      }

    }
  }

  .movie {

    &__title {
      height: 100vh;
      background: 50% no-repeat;
      background-size: cover;
      @include flexbox();
      @include align-items(center);
      @include justify-content(center);
      border: 100px solid $white;
      @include box-sizing(border-box);

      h1 {
        font-weight: 700;
        color: $white;
        font-size: 60px;
        max-width: 700px;
        text-align: center;
        text-shadow: 0 2px 4px rgba(0, 0, 0, .5);
      }

      @media #{$mobile} {
        border: none;
        border-top: 60px solid $white;
      }
    }

    &__description {
      max-width: 1250px;
      margin: 100px auto 0;

      .left {
        width: 100%;
        max-width: 400px;
        text-align: right;
      }

      .right {
        width: 100%;
        max-width: 600px;
      }

      &--part1 {
        @include flexbox();
        @include justify-content(space-between);
        margin-bottom: 100px;

        &--affiche {
          margin-bottom: 100px;
        }

        h2 {
          font-size: 50px;
          font-weight: 900;
          margin-bottom: 100px;
          position: relative;

          &:after {
            content: '';
            position: absolute;
            bottom: -20px;
            height: 50px;
            width: 400px;
            left: -30px;
            background: #F7F7F7;
            z-index: -1;

            @media screen and(max-width: 400px) {
              width: 100%;
            }
          }
        }

        &--synopsis {
          line-height: 40px;
          font-size: 18px;
          font-weight: 300;
        }

        @media #{$mobile} {
          flex-direction: column;
          align-items: center;
        }
      }

      &--part2 {
        margin-bottom: 200px;

        .movie__description--info {
          @include flexbox();
          @include align-items(flex-start);
          @include justify-content(space-between);
          font-size: 20px;
          font-weight: 500;
          margin-bottom: 70px;
          line-height: 40px;

          &:last-of-type {
            margin-bottom: 0px;
          }
        }

      }

      &--info {
        font-weight: 900;
        font-size: 23px;
        margin-bottom: 50px;

        span {
          width: 100%;
          color: $grey;
          font-size: 12px;
          font-weight: 900;
          text-transform: uppercase;
          display: block;
          margin-bottom: 5px;
        }


        @media #{$mobile} {
          text-align: center;
        }
      }

      @media #{$mobile} {
        padding: 15px;
      }

    }

  }
</style>
