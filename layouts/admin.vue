<template>
  <div class="root">
    <nav>
      <div class="admin-logo">ADMIN</div>
      <div class="admin-menu" ref="adminMenu">
        <div class="menu-item" @click="mainPage" id="/">Главная</div>
        <div class="menu-item" @click="users" id="/users">Пользователи</div>
        <div class="menu-item" @click="settings" id="/settings">Настройки</div>
        <div class="menu-item" @click="accounts" id ="/accounts">Аккаунты</div>
        <div class="menu-item" @click="payments" id="/payments">Выводы</div>
        <div class="menu-item" @click="logOut">Выйти</div>
      </div>
    </nav>

    <div class="page-content">
      <Nuxt/>
    </div>
  </div>
</template>

<script>
export default {
  name: "admin",
  data() {
    return {
      currentRoute : ''
    }
  },
  mounted() {
    this.activateRoute()
  },
  watch: {
    '$route.path' (value) {
      this.currentRoute = value

      this.activateRoute()
    }
  },
  methods: {
    activateRoute() {
      let routes = this.$refs.adminMenu.getElementsByClassName('menu-item')

      for (let route of routes) {
        if (route.id === this.$route.path) {
          route.style.color = '#2077FF'
        }
        else {
          route.style.color = ''
        }
      }
    },
    mainPage(){
      this.$router.replace('/')
    },
    users() {
      this.$router.replace('/users')
    },
    settings() {
      this.$router.replace('/settings')
    },
    accounts() {
      this.$router.replace('/accounts')
    },
    payments() {
      this.$router.replace('/payments')
    },
    logOut() {
      this.$cookies.remove('JWT_TOKEN')
      this.$router.replace('/auth')
    }
  }
}
</script>

<style scoped>

nav {
  border-bottom : 2px solid #3C4655;
  @apply w-screen fixed top-0;
}

.root {
  @apply bg-[#001434] w-screen h-screen;
}

.page-content {
  @apply relative top-[53px]
}

.admin-menu {
  @apply flex py-4 mx-auto w-fit top-0;
}

.admin-menu .menu-item {
  font-weight: 400;
  @apply text-[#91969F] cursor-pointer px-[25px];
}

.menu-item:hover {
  @apply text-[#2077FF]
}

.admin-logo {
  background: linear-gradient(95.94deg, #00C9FF 2.47%, #92FE9D 100%);
  color : transparent;
  letter-spacing: 0.145em;
  background-clip: text;
  -webkit-background-clip: text;
  @apply py-2 text-2xl font-bold w-[300px] text-center fixed;
}

</style>
