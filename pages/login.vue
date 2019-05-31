<template>

  <div>
    <form action="" @submit.prevent="addUser">
      <div class="formContent">
        <h2>Welcome back,</h2>
        <!--<h2><span>{{ username }}</span></h2>-->
        <input type="email" placeholder="Email adress" autofocus required v-model="userForm.email">
        <input type="password" placeholder="Password" required v-model="userForm.password">
        <button type="submit"></button>
      </div>
    </form>
  </div>

</template>

<script>

  export default {
    name: "login",
    data() {
      return {
        username: 'Will',
        userForm: {
          email: '',
          password: ''
        }
      }
    },
    methods: {
      async addUser() {
        await this.$auth.login({
          data: this.userForm
        });
        this.$router.push({
          path: '/'
        });
      }
    }
  }
</script>

<style scoped lang="scss">

  @import "@/assets/scss/style.scss";

  form{
    width: 500px;
    margin: 0 auto;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    box-shadow: 0 19px 38px rgba(0,0,0,0.30), 0 15px 12px rgba(0,0,0,0.22);
    padding: 50px 0;

    & *{
      box-sizing: border-box;
    }

    & .formContent{
      width: 300px;
      margin: 0 auto;

      & h2{
        font-family: $Circular;
        color: $black;
        font-weight: normal;
        margin-bottom: 10px;
        font-size: 40px;

        & span{
          font-weight: bold;
        }

        &:last-of-type{
          margin-bottom:30px;
        }
      }

      & input[type="text"],
      & input[type="email"],
      & input[type="password"]{
        appearance: none;
        -webkit-appearance: none;
        border: none;
        border-bottom: solid 2px #BEB9C5;
        display: block;
        width: 100%;
        height: 47px;
        font-family: $Circular;
        color: $black;
        font-size: 18px;
        padding: 0 5px;
        outline: none;
        margin-bottom: 10px;

        &::placeholder{
          font-family: $Circular;
          color: #BEB9C5;
          font-size: 18px;
        }
      }

      & button{
        appearance: none;
        -webkit-appearance: none;
        border: none;
        margin: 50px 0 0 auto;
        display: block;
        width: 60px;
        height: 60px;
        background: $blue url(../assets/img/right-arrowW.svg);
        background-repeat: no-repeat;
        background-size: 30px;
        background-position: center center;
        border-radius: 18px;
        cursor: pointer;
      }

      @media #{$mobile} {
        width: calc( 100% - 40px);
      }
    }

    @media #{$mobile} {
      width: calc( 100% - 40px);
    }
  }

</style>
