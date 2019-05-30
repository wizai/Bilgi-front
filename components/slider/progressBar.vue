<template>

  <div class="slider-navbar">
    <span>{{sliderCurrent}}</span>
    <div class="slider-navbar__progressbar">
      <div class="slider-navbar__progressbar--progress" ref="progressBar" :style="{ width: progress}"></div>
    </div>
    <span>{{sliderMax}}</span>
  </div>

</template>

<script>
  export default {
    name: "progressBar",
    props: {
      sliderCurrent: "",
      sliderMax: "",
      progress: ""
    }
  }
</script>


<style lang="scss">

  @import "@/assets/scss/style.scss";

  .slider-navbar {
    position: absolute;
    bottom: 100px;
    left: 0;
    width: 100%;
    @include flexbox();
    @include align-items(center);
    @include justify-content(center);

    span {
      font-weight: 700;
      margin: 0 15px;
    }

    &__progressbar {
      position: relative;
      width: 150px;
      height: 1px;
      background-color: #fff;

      &--progress {
        position: absolute;
        top: -1px;
        left: 0;
        height: 3px;
        width: 0%;
        background-color: $blue;
      }

    }

    @media #{$mobile} {
      bottom: 50px;
    }

  }

</style>
