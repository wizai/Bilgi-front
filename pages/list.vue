<template>
    <div>
        <section class="list">
            <div class="list__container">
                <h1>Gallery</h1>
                <div class="gallery">
                    <div class="gallery__item">
                        <a href="">
                            <figure class="gallery__item__img">
                                <img src="" alt="">
                            </figure>
                            <h2 class="gallery__item__title">Titre</h2>
                            <h2 class="gallery__item__date">05/05/2000</h2>
                            <p class="gallery__item__content">Lorem ipsum dolor sit amet consectetur adipisicing elit. Placeat, doloribus labore? Vitae iusto veritatis similique. Rerum ullam animi aperiam blanditiis tempore, aliquid possimus perspiciatis odit, debitis repudiandae enim quibusdam nam.</p>
                        </a>
                    </div>
                    <div class="gallery__item">
                        <a href="">
                            <figure class="gallery__item__img">
                                <img src="" alt="">
                            </figure>
                            <h2 class="gallery__item__title">Titre</h2>
                            <h2 class="gallery__item__date">05/05/2000</h2>
                            <p class="gallery__item__content">Lorem ipsum dolor sit amet consectetur adipisicing elit. Placeat, doloribus labore? Vitae iusto veritatis similique. Rerum ullam animi aperiam blanditiis tempore, aliquid possimus perspiciatis odit, debitis repudiandae enim quibusdam nam.</p>
                        </a>
                    </div>
                    <div class="gallery__item">
                        <a href="">
                            <figure class="gallery__item__img">
                                <img src="" alt="">
                            </figure>
                            <h2 class="gallery__item__title">Titre</h2>
                            <h2 class="gallery__item__date">05/05/2000</h2>
                            <p class="gallery__item__content">Lorem ipsum dolor sit amet consectetur adipisicing elit. Placeat, doloribus labore? Vitae iusto veritatis similique. Rerum ullam animi aperiam blanditiis tempore, aliquid possimus perspiciatis odit, debitis repudiandae enim quibusdam nam.</p>
                        </a>
                    </div>
                    <div class="gallery__item">
                        <a href="">
                            <figure class="gallery__item__img">
                                <img src="" alt="">
                            </figure>
                            <h2 class="gallery__item__title">Titre</h2>
                            <h2 class="gallery__item__date">05/05/2000</h2>
                            <p class="gallery__item__content">Lorem ipsum dolor sit amet consectetur adipisicing elit. Placeat, doloribus labore? Vitae iusto veritatis similique. Rerum ullam animi aperiam blanditiis tempore, aliquid possimus perspiciatis odit, debitis repudiandae enim quibusdam nam.</p>
                        </a>
                    </div>
                    <div class="gallery__item">
                        <a href="">
                            <figure class="gallery__item__img">
                                <img src="" alt="">
                            </figure>
                            <h2 class="gallery__item__title">Titre</h2>
                            <h2 class="gallery__item__date">05/05/2000</h2>
                            <p class="gallery__item__content">Lorem ipsum dolor sit amet consectetur adipisicing elit. Placeat, doloribus labore? Vitae iusto veritatis similique. Rerum ullam animi aperiam blanditiis tempore, aliquid possimus perspiciatis odit, debitis repudiandae enim quibusdam nam.</p>
                        </a>
                    </div>
                    <div class="gallery__item">
                        <a href="">
                            <figure class="gallery__item__img">
                                <img src="" alt="">
                            </figure>
                            <h2 class="gallery__item__title">Titre</h2>
                            <h2 class="gallery__item__date">05/05/2000</h2>
                            <p class="gallery__item__content">Lorem ipsum dolor sit amet consectetur adipisicing elit. Placeat, doloribus labore? Vitae iusto veritatis similique. Rerum ullam animi aperiam blanditiis tempore, aliquid possimus perspiciatis odit, debitis repudiandae enim quibusdam nam.</p>
                        </a>
                    </div>
                    <div class="gallery__item">
                        <a href="">
                            <figure class="gallery__item__img">
                                <img src="" alt="">
                            </figure>
                            <h2 class="gallery__item__title">Titre</h2>
                            <h2 class="gallery__item__date">05/05/2000</h2>
                            <p class="gallery__item__content">Lorem ipsum dolor sit amet consectetur adipisicing elit. Placeat, doloribus labore? Vitae iusto veritatis similique. Rerum ullam animi aperiam blanditiis tempore, aliquid possimus perspiciatis odit, debitis repudiandae enim quibusdam nam.</p>
                        </a>
                    </div>
                    <div class="gallery__item">
                        <a href="">
                            <figure class="gallery__item__img">
                                <img src="" alt="">
                            </figure>
                            <h2 class="gallery__item__title">Titre</h2>
                            <h2 class="gallery__item__date">05/05/2000</h2>
                            <p class="gallery__item__content">Lorem ipsum dolor sit amet consectetur adipisicing elit. Placeat, doloribus labore? Vitae iusto veritatis similique. Rerum ullam animi aperiam blanditiis tempore, aliquid possimus perspiciatis odit, debitis repudiandae enim quibusdam nam.</p>
                        </a>
                    </div>
                </div>
            </div>
        </section>
    </div>
</template>

<script>

  import axios from "axios";

  export default {

    name: "list",

    methods: {

    }
  }
</script>


<style lang="scss">

  @import "@/assets/scss/style.scss";

  .list {
    position: relative;

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

      & .gallery{
          display: flex;
          align-items: center;
          flex-wrap: wrap;

          &__item{
              width: calc( 100% / 3 - 14px );
              margin-right: 20px;
              margin-bottom: 20px;

              &:nth-child(3n){
                  margin-right: 0;
              }

              & a{
                  color: $black;
              }

            @media #{$mobile} {
                width: 100%;
            }
          }
      }
    }
  }

</style>
