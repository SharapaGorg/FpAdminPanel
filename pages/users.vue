<template>
  <div>
    <div class="users-headers">
      <div class="users-count">Пользователи ({{ users.length }})</div>

      <div class="field-container">
        <input
          class='find-field'
          placeholder="Найти пользователя"
          v-model="searchedUser"
        />

        <img src="../static/zoom.svg" class="zoom"/>
      </div>
    </div>

    <div class="gradient-line"></div>

    <div class="users">
      <div class="user">
        <div class="gray-color">User-id</div>
        <div class="gray-color">Имя</div>
        <div class="gray-color">Username</div>
        <div class="gray-color">Баланс</div>
      </div>
      <div
        class="user"
        v-for="user in filteredUsers"
        :key="user.id"
      >
        <div>{{ user.id }}</div>
        <div>{{ user.name }}</div>
        <div>{{ user.username }}</div>
        <div>{{ user.balance }}</div>
        <div class="user-button" @click="toUser(user.id)">Перейти</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "users",
  layout: 'admin',
  data() {
    return {
      users: [],
      filteredUsers: [],
      searchedUser: ''
    }
  },
  async mounted() {
    this.users = await this.getUsers()
    this.filteredUsers = this.users
  },
  watch: {
    searchedUser(value) {
      this.filteredUsers = this.users.filter(x => {
        return x.username.includes(value) || x.name.includes(value) || x.id.toString().includes(value) || x.balance.toString().includes(value)
      })
    }
  },
  methods: {
    toUser(userID) {
      this.$router.replace(`/selectedUser/${userID}`)
    },
    async getUsers() {
      return [{
        id: 815800615,
        name: "Exedna",
        username: "exedna",
        balance: 200
      }]
    }
  }
}
</script>

<style scoped>

.users-headers {
  @apply py-6 grid grid-cols-2 justify-items-end md:w-2/3 mx-auto;
}

.users-count {
  @apply text-left w-full py-2;
}

.field-container {
  @apply flex;
}

.zoom {
  transform: translatex(-6px);

  @apply z-10
}

.find-field {
  transform: translatex(19px);
  @apply rounded-md pl-3 pr-8 py-3 outline-none block bg-[#3C4655] border-none;
  @apply w-[200px]
}

.gradient-line {
  box-shadow: 0px 0px 4px #0FBA56;
  background: linear-gradient(95.94deg, #00C9FF 2.47%, #92FE9D 100%);
  @apply w-2/3 h-[2px] mx-auto mb-4;
}

.users {
  @apply w-2/3 mx-auto;
}

.user {
  @apply grid grid-cols-5 justify-items-center my-3;
}

.gray-color {
  color: #91969F
}

.user-button {
  @apply bg-[#4D67F0] px-5 py-1 rounded-md cursor-pointer;
  @apply relative top-[-5px]
}

</style>
