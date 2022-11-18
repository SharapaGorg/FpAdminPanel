<template>
  <div class="accounts-container">
    <div class="users-headers">
      <div class="sort-header">Сортировка</div>
    </div>

    <div class="gradient-line"></div>

    <div class="users">
      <div class="user">
        <div class="gray-color">Login</div>
        <div class="gray-color">Пользователь</div>
        <div class="gray-color">Статус</div>
        <div class="field-container">
          <input
            class='find-field'
            placeholder="Поиск..."
            v-model="searchedUser"
          />

          <img src="../static/zoom.svg" class="zoom"/>
        </div>
      </div>
      <div
        class="user"
        v-for="user in filteredUsers"
        :key="user.id"
      >
        <div>{{ user.login }}</div>
        <div>{{ user.username }}</div>
        <div>{{ user.status }}</div>
        <div class="account-settings">
          <img src="../static/gears.svg"/>
        </div>
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
    }
  },
  methods: {
    async getUsers() {
      return [
        {
          login: "TestLogin1",
          username: "Exedna",
          status: "Верифицирован"
        },
        {
          login : "TestLogin2",
          username : "Отсутствует",
          status : "Загружен"
        }
      ]
    }
  }
}
</script>

<style scoped>

.accounts-container {
  @apply rounded-lg lg:w-2/3 w-[95%] mx-auto bg-[#0D2441];
  @apply px-4 py-3 relative top-[30px]
}

.users-headers {
  @apply pb-2 grid grid-cols-2 justify-items-start w-full;
}

.sort-header {
  @apply text-left w-fit py-2 pl-3;
}

.field-container {
  @apply flex;
}

.zoom {
  transform: translatex(-6px) translateY(-4px);

  @apply z-10
}

.find-field {
  transform: translateX(19px);
  @apply rounded-md pl-3 pr-8 py-2 outline-none block bg-[#3C4655] border-none;
  @apply w-[150px] relative top-[-5px]
}

.gradient-line {
  box-shadow: 0 0 4px #0FBA56;
  background: linear-gradient(95.94deg, #00C9FF 2.47%, #92FE9D 100%);
  @apply w-full h-[2px] mx-auto mb-7;
}

.users {
  @apply w-full;
}

.user {
  @apply grid grid-cols-4 justify-items-center my-3;
}

.gray-color {
  color: #91969F
}

.account-settings {
  @apply flex;
}

.account-settings img {
  @apply h-[25px] w-[25px] cursor-pointer;
}

</style>
