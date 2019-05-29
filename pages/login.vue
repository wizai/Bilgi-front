<template>

  <div>
    <form action="" @submit.prevent="addUser">
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
    name: "login",
    data() {
      return {
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

<style scoped>

</style>
