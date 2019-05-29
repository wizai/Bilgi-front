<template>
  <section class="article">
    <div class="article__container">
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

  .article {


    &__container {
      max-width: 900px;
      margin: 0 auto 100px;
      padding: 15px;
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

      .buttonContainer{
        text-align: center;
        margin: 100px auto 0;
        @media #{$mobile} {
          margin: 60px auto 0;
        }
      }
      .button{
        text-decoration: none;
        color: $black;
        position: relative;
        display: inline-block;
        font-weight: 700;

        &:hover{

          .button__text:before{
            @include transform(scaleX(0))
          }
          .button__text:after{
            @include transform(scaleX(1));
            transition-delay: .1s;
          }
          .button__circle{
            @include transform(translate(130%,-50%));
            @include transition(all .5s cubic-bezier(.54,.1,0,.99));
          }

          .arrow{
            @include transform(scaleX(1));
            transition-delay: .25s;
          }

        }

        &__text{
          position: relative;
          &:before, &:after{
            content: "";
            position: absolute;
            top: 50%;
            display: inline-block;
            width: 16px;
            height: 2px;
            background-color: $black;
          }
          &:before{
            right: calc(100% + 6px);
            -webkit-transform-origin: right;
            transform-origin: right;
            @include transition(all .5s cubic-bezier(.54,.1,0,.99));
          }
          &:after{
            left: calc(100% + 6px);
            -webkit-transform-origin: left;
            transform-origin: left;
            @include transform(scaleX(0));
            @include transition(all .5s cubic-bezier(.54,.1,0,.99));
          }
        }

        .arrow{
          width: 16px;
          height: 16px;
          position: absolute;
          top: calc(50% - 5px);
          right: -36px;
          -webkit-transform-origin: left;
          transform-origin: left;
          @include transform(scaleX(0));
          @include transition(all .4s cubic-bezier(.54,.1,0,.99));
          -webkit-transition-delay: 0s;
          transition-delay: 0s;
        }

        &__circle{
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
          @include transition(all .7s cubic-bezier(.54,.1,0,.99));

          &--block{
            width: 60px;
            height: 60px;
            -webkit-border-radius: 100%;
            -moz-border-radius: 100%;
            border-radius: 100%;
            @include transition(all .7s cubic-bezier(.54,.1,0,.99));
            background-color: #eaeaea;
            @include transform(matrix(1, 0, 0, 1, 0, 0));
          }
        }
      }

    }

  }

</style>
