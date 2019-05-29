<template>
  <div>
    <form action="" @submit.prevent="registerUser">
      <label for="">Name</label>
      <input type="text" placeholder="Name" autofocus required v-model="userForm.name">
      <label for="">Email</label>
      <input type="email" placeholder="email" autofocus required v-model="userForm.email">
      <label for="">password</label>
      <input type="password" placeholder="password" required v-model="userForm.password">
      <button type="submit">Login</button>
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
          password: ''
        }
      }
    },
    methods: {
      async registerUser() {
        await this.$axios.post('register', this.userForm);
        this.$auth.login({
          data: {
            email: this.userForm.email,
            password: this.userForm.password
          }
        });
        this.$router.push({
          path: '/'
        });
      }
    }
  }
</script>

<style scoped>

</style>
