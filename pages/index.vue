<template>
  <section class="page-homepage">
    <header>
      <nuxt-link :to="{ name: 'login' }" class="nav-link">
        Login
      </nuxt-link>
      <nuxt-link :to="{ name: 'register' }" class="nav-link">
        Register
      </nuxt-link>
      <a href="" @click.prevent="logout">Sign Out</a>
    </header>
    <div>
      <div class="center">
        <div class="centerBis">
          <p v-if="loggedIn">
            Hello {{ user.name }}
          </p>
          <p v-if="!loggedIn">
            Please sign in
          </p>
        </div>
      </div>
    </div>
  </section>
</template>

<script>

  export default {
    methods: {
      logout() {
        this.$auth.logout();
      }
    }
  }

</script>
<style>
  .page-homepage{
    background: radial-gradient(#183E80, #001447);
    background-size: cover;
    height: 100vh;
    width: 100%;
    color: #ffffff;
    position: relative;
  }
  .center{
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    height: 300px;
    width: 300px;
    background-color: #0D2A66;
    border-radius: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
  }
  .centerBis{
    background-color: orangered;
    width: 150px;
    height: 150px;
    border-radius: 100%;
  }

</style>
