<template>

  <div class="header">

    <header>

      <div class="header__container" v-bind:class="{ 'color-nav': $route.path == '/' }">
        <div class="navMobileContainer" >
          <div class="menuBurger"
          v-bind:class="{ change: openMenuBurger }"
          v-on:click="openMenuBurger = !openMenuBurger, openNav()"
          >
            <div class="bar1"></div>
            <div class="bar2"></div>
            <div class="bar3"></div>
          </div>
        </div>
        <nav class="nav">
          <nuxt-link to="/" class="logo">Bilgi</nuxt-link>
          <div v-if="loggedIn" class="logIn">
            <div class="user"
            v-bind:class="{ open: active }"
            v-on:click="active = !active"
            >
              <div class="user__img" :style="{ background: 'url(' + user.avatar.name + ') center top / cover'}"></div>
              <p class="user__name">Bonjour, {{ user.name }}</p>
              <div class="user__arrow"></div>
              <div class="user__nav">
                <ul>
                  <li>
                    <a href="#">My profile</a>
                    <a href="#">Gallery</a>
                    <a href="" @click.prevent="logout">Sign Out</a>
                  </li>
                </ul>
              </div>
            </div>
          </div>
          <div v-else>
            <nuxt-link to="/login" class="sign in">Sign in</nuxt-link>
            <nuxt-link to="/register" class="sign up">Sign up</nuxt-link>
          </div>
        </nav>
      </div>

    </header>

  </div>

</template>

<script>

  export default {
    name: "Header",

    data() {
      return{
        active: false,
        openMenuBurger: false
      }
    },

    methods: {
      logout() {
        this.$auth.logout();
      },
      openNav() {
        var nav = document.querySelector('.nav');
        nav.classList.toggle("open");
      }

    }
  }

</script>

<style lang="scss">

  @import "@/assets/scss/style.scss";

  .header {

    header{
      position: fixed;
      width: 100%;
      z-index: 4;
    }

    &__container {
      position: relative;
      height: 100px;
      @include flexbox();
      @include align-items(center);
      @include justify-content(space-between);
      @include box-sizing(border-box);
      width: 100%;
      padding: 0 100px;
      background-color: $white;

      &.color-nav{
        background-color: transparent;
        & nav {
          .logIn{
            p{
              color: $white;
            }
            a{
              background-color: $white;
              color: $black;
            }
            .user__arrow{
              border: 2px solid $white;
              border-left: 0px;
              border-top: 0px;
            }
          }
          & a{
            &.logo,
            &.sign{
              color: #fff;
              &.up{
                background-color: #fff;
                color: black;
              }
            }
          }
        }

        & .navMobileContainer{
          z-index: 6;

          & .menuBurger{
            & .bar1,
            & .bar2,
            & .bar3{
              background-color: $white;
            }
          }
        }
      }

      & .navMobileContainer{
        display: none;

        @media #{$mobile} {
          display: block;
          z-index: 55;
        }

        & .menuBurger{
          & .bar1,
          & .bar2,
          & .bar3{
            width: 35px;
            height: 3px;
            background-color: $white;
            margin: 6px 0;
            border-radius: 5px;
            transition: .4s ease;
          }

          &.change{
             & .bar1 {
                -webkit-transform: rotate(-45deg) translate(-5px, 6px);
                transform: rotate(-45deg) translate(-5px, 6px);
              }

              & .bar2 {opacity: 0;}

              & .bar3 {
                -webkit-transform: rotate(45deg) translate(-7px, -8px);
                transform: rotate(45deg) translate(-7px, -8px);
              }
          }
        }
      }

      &__profil{
        position: absolute;
        top: 0;
        right: 0;
        display: flex;
        flex-direction: column;
        justify-content: center;
        background-color: $white;

        & li{
          text-align: center;
        }
      }

      @media #{$mobile} {
        padding: 0 50px;
      }

    }

    nav{
      @include flexbox();
      @include justify-content(space-between);
      width: 100%;

      & div{
        @media #{$mobile} {
          display: flex;
          flex-direction: column;
        }
      }

      .user{
        @include flexbox();
        @include align-items(center);
        position: relative;
        &__img{
          height: 30px;
          width: 30px;
          margin-right: 20px;
          -webkit-border-radius: 100%;
          -moz-border-radius: 100%;
          border-radius: 100%;
          background: 50% no-repeat;
          -webkit-background-size: cover;
          background-size: cover;
        }
        &__arrow{
          margin-left: 10px;
          height: 6px;
          width: 6px;
          border: 2px solid $black;
          @include transform(rotate(45deg));
          border-left: 0px;
          border-top: 0px;
          display: inline-block;

          @media #{$mobile} {
            margin-top: -15px;
          }
        }

        &__nav{
          position: absolute;
          width: 100%;
          min-width: 110px;
          display: none;
          flex-direction: column;
          top: 100%;
          left: 50%;
          transform: translate(-50%, 8px);

          & li{

            & a{
              width: 100%;
              border-radius: 0;
              margin-left: 0;
              padding: 0;
              text-align: center;
              padding: 6px 0;
              color: $black!important;
              background-color: $white;

              @media #{$mobile} {
                margin-bottom: 0;
              }
            }
          }
        }

        &.open{

          & .user__nav{
            display: flex;
          }
        }
      }

      .logIn{
        p, a{
          font-weight: 700;
          color: $black;
          display: inline-block;
          @media #{$mobile} {
            display: block;
            text-align: center;
            margin-bottom: 20px;
            color: $white;
          }
        }
        a{
          margin-left: 20px;
          display: inline-block;
          padding: 6px 20px;
          border-radius: 20px;
          color: $white;
          background-color: $black;
          @media #{$mobile} {
            width: 100px;
            text-align: center;
            margin-left: 0px;
          }
        }
      }

      & a{
        font-weight: bold;

        &.logo{
          font-size: 18px;
          color: $black;

          @media #{$mobile} {
            margin-bottom: 20px;
            color: $white;
          }
        }

        &.sign{
          display: inline-block;
          padding: 6px 20px;
          border-radius: 20px;
          color: $black;

          &.in{

            @media #{$mobile} {
              margin-bottom: 20px;
            }
          }

          &.up{
            background-color: $black;
            color: $white;
          }

          @media #{$mobile} {
            width: 100px;
            text-align: center;
          }
        }
      }

      @media #{$mobile} {
        position: absolute;
        width: 100%;
        height: 100vh;
        background: radial-gradient(#183E80, #001447);
        left: 0;
        top: 0;
        transform: translateX(-100%);
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        transition: .4s ease;
      }
    }

    .nav{
      &.open{
        transform: translateX(0);
      }
    }
  }

</style>
