<template>

  <div class="header">

    <header>

      <div class="header__container">
        <nav>
          <nuxt-link to="/" class="logo">Bilgi</nuxt-link>
          <div>
            <nuxt-link to="/login" class="sign in">Sign in</nuxt-link>
            <nuxt-link to="register" class="sign up">Sign up</nuxt-link>
          </div>
        </nav>
      </div>

    </header>

  </div>

</template>

<script>

  export default {
    name: "Header",
  }

</script>

<style lang="scss">

  @import "@/assets/scss/style.scss";

  .header {

    header{
      position: relative;
    }

    &__container {
      height: 100px;
      @include flexbox();
      @include align-items(center);
      @include justify-content(space-between);
      @include box-sizing(border-box);
      width: 100%;
      padding: 0 100px;

    }

    nav{
      @include flexbox();
      @include justify-content(space-between);
      width: 100%;

      & a{
        font-weight: bold;

        &.logo{
          font-size: 18px;
          color: $black;
        }

        &.sign{
          display: inline-block;
          padding: 6px 20px;
          border-radius: 20px;
          color: $black;

          &.up{
            background-color: $black;
            color: $white;
          }
        }
      }
    }
  }

</style>
