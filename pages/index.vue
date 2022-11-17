<template>
  <div class="main-screen">
  </div>
</template>

<script>
export default {
  name: 'IndexPage',
  created() {
    let token = this.$cookies.get('JWT_TOKEN')
    if (!this.checkToken(token)) {
      this.$router.push('auth')
    }
  },
  methods: {
    checkToken(token) {
      // test auth
      return false
    }
  }
}
</script>

<style>

.main-screen {
  @apply text-4xl font-bold text-center w-full;
}

</style>
