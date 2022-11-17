<template>
  <div class="auth-form">
    <input
      class="auth-input"
      placeholder="Password"
      v-model="password"
      type="password"
    />
    <div class="auth-button" @click="login">Login</div>
  </div>
</template>

<script>
export default {
  name: "auth",
  data() {
    return {
      password : ''
    }
  },
  mounted() {
  },
  methods: {
    login() {
        console.log(`Trying to log in with (${this.password})...`)
        this.$router.replace('/accounts')
    }
  }
}
</script>

<style scoped>

.auth-form {
  top : 30vh;
  @apply w-[350px] rounded-md bg-[#0D2441] mx-auto;
  @apply relative py-6;
}

.auth-input {
  @apply bg-[#3C4655] w-[300px] mx-auto block outline-none;
  @apply py-2 rounded-md border-none pl-3 text-[20px];
}

.auth-button {
  @apply bg-[#4D67F0] rounded-md text-center mt-4 w-[300px];
  @apply py-2 mx-auto px-1.5 cursor-pointer;
}

</style>
