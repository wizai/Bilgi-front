<template>
  <div>
    <Header/>
    <nuxt :key="$route.fullPath"/>
  </div>
</template>

<script>
  import Header from "~/components/Header/Header.vue";

  export default {
    components: {
      Header,
    }

  }

</script>


<style>
  .page-enter-active,
  .page-leave-active {
    opacity: 1;
    transition: opacity .25s;
    animation-duration: .3s;
    animation-fill-mode: both;
  }

  .page-enter-active {
    animation-name: pageFadeInUp;
  }

  .page-leave-active {
    animation-name: pageFadeOutDown;
  }

  .page-enter, .page-leave-to {
    opacity: 0;
  }


  @-webkit-keyframes pageFadeInUp {
    0% {
      opacity: 0;
      transform: translate3d(0, 1.25%, 0);
    }

    to {
      opacity: 1;
      transform: none;
    }
  }

  @-webkit-keyframes pageFadeOutDown {
    0% {
      opacity: 1;
    }

    to {
      opacity: 0;
      transform: translate3d(0, 1.25%, 0);
    }
  }
</style>
