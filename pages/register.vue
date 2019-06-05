<template>
  <div>
    <form action="" @submit.prevent="registerUser" enctype="multipart/form-data">
      <div class="formContent">
        <h2>Hello <span>Buddy</span>,</h2>
        <p>Enter your informations below</p>
        <input type="text" placeholder="Name" autofocus required v-model="userForm.name">
        <input type="email" placeholder="Email adress" autofocus required v-model="userForm.email">
        <input type="password" placeholder="Password" required v-model="userForm.password">
        <input type="text" placeholder="Hobbies" v-model="userForm.hobby">
        <p class="info">Use , to input a hobby.</p>
        <label class="label-file" for="avatar">Choose an image</label>
        <input type="file" ref="avatar" @change="processFile($event)" id="avatar">
        <div class="chooseHobby">
          <div class='tagHere'></div>
          <input type="text" autofocus/>
        </div>
        <button type="submit"></button>
      </div>
    </form>
  </div>
</template>

<script>
  export default {
    name: "register",
    data() {
      return {
        userForm: {
          name: '',
          email: '',
          password: '',
          hobby: [],
          avatar: '',
        }
      }
    },
    methods: {
      async registerUser() {
        let formData = new FormData();
        formData.append('name', this.userForm.name);
        formData.append('email', this.userForm.email);
        formData.append('password', this.userForm.password);
        formData.append('hobby', JSON.stringify(this.userForm.hobby));
        formData.append('avatar', this.userForm.avatar);

        await this.$axios.post('register', formData,
          {
            headers: {
              'Content-Type': 'multipart/form-data'
            }
          }
        );
        this.$auth.login({
          data: {
            name: this.userForm.name,
            email: this.userForm.email,
            password: this.userForm.password,
            hobby: this.userForm.hobby,
            avatar: this.userForm.file
          }
        });
        console.log(this.userForm);
        this.$router.push({
          path: '/'
        });
      },

      processFile() {
        console.log(this)
        this.userForm.avatar = this.$refs.avatar.files[0];
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
      }

      & p{
        font-family: $Circular;
        color: $black;
        font-weight: normal;
        margin-bottom: 30px;
        font-size: 16px;
        &.info{
          font-size: 10px;
          font-style: italic;
          margin-bottom: 10px;
        }
      }

      & input[type="text"],
      & input[type="email"],
      & input[type="password"],
      & .label-file{
        appearance: none;
        -webkit-appearance: none;
        border: none;
        border-bottom: solid 2px #BEB9C5;
        display: block;
        width: 100%;
        height: 47px;
        line-height: 47px;
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

      input[type="file"] {
          display: none;
      }

      .chooseHobby{
        input{
          outline: none;
          width: auto;
          border: 0;
          float: left;
          padding: 8px;
          background: none;
          & a {
            color: #000;
            padding-right: 10px;
            padding-left:5px;
            padding-top: 5px;
            padding-bottom: 5px;
            margin-right: 5px;
          }

          & span {
            padding-right: 10px;
            padding-left: 0px;
            padding-top: 5px;
            padding-bottom: 5px;
          }
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
