<template>
  <div>

    <div class="form-container" v-show="editingBalance" @click.self="editingBalance = false">
      <div class="balance-form">
        <div class="currency">₽</div>
        <input
          class="balance-input"
          :placeholder="user.balance"
          v-model="newBalance"
          type="number"
        />

        <div class="save-balance-button" @click="saveBalance">Сохранить</div>
      </div>
    </div>

    <div class="user-header">Пользователь <span style="color:#4D67F0">{{ user.name }}</span></div>
    <div class="info-blocks">
      <div class="add-info-container">
        <div>
          <div class="info-block" style="margin-bottom : 1rem" @click="copyToClipBoard(user.username)">
            @{{ user.username }} <img src="../../static/copy.svg" class="buffer"/>
          </div>
          <div class="info-block" @click="copyToClipBoard(user.id)">
            {{ user.id }}<img src="../../static/copy.svg" class="buffer"/>
          </div>
        </div>

        <div class="balance-block">
          <div class="balance">{{ user.balance }} ₽</div>
          <div class="edit-balance" @click="editingBalance = true">Изменить</div>
        </div>
      </div>

      <div class="messages-info">
        <div
          class="message-block"
          style="margin-bottom : 1rem"
        >
          <span>Первое сообщение:</span> <div class="message">12-04-2022 14:30</div>
        </div>
        <div
          class="message-block"
        >
          <span>Последнее сообщение:</span> <div class="message">07-11-2022 13:16</div>
        </div>
      </div>
    </div>

    <div class="actions">
      <div class="edit-balance">Забанить</div>
      <div class="edit-balance">Просмотреть логи</div>
      <div class="edit-balance">Скачать логи</div>
      <div class="edit-balance">Скачать аккаунты</div>
    </div>
  </div>
</template>

<script>
export default {
  name: "_id",
  layout: 'admin',
  data() {
    return {
      user: {},
      newBalance : 200,
      editingBalance : false
    }
  },
  async mounted() {
    this.user = await this.getUser(this.$route.params.id)
    this.newBalance = this.user.balance
  },
  methods: {
    async getUser(id) {
      return {
        id: 815800615,
        name: "Exedna",
        username: "exedna",
        balance: 200
      }
    },
    saveBalance() {
      console.log(`New balance : ${this.newBalance}`)
      this.editingBalance = false
    },
    copyToClipBoard(text) {
      navigator.clipboard.writeText(text)
    }
  }
}
</script>

<style scoped>

.user-header {
  @apply text-2xl w-fit mx-auto py-4;
}

.info-blocks {
  @apply flex w-fit mx-auto mt-10;
}

.info-block {
  border: 2px solid #3C4655;
  font-weight: 400;
  @apply bg-[#031840] px-10 py-3 rounded-md;
  @apply cursor-pointer;
}

.buffer {
  transform : translateX(5px) translateY(3px);
  @apply h-[15px] absolute
}

.add-info-container {
  @apply flex;
}

.balance-block {
  border: 2px solid #3C4655;
  @apply bg-[#031840] px-3 rounded-md ml-4;
}

.balance {
  @apply w-[130px] text-center mt-5;
}

.edit-balance {
  @apply bg-[#4D67F0] px-5 py-1 rounded-md cursor-pointer;
  @apply text-center mt-8;
}

.messages-info {
  @apply ml-4
}

.message-block {
  border: 2px solid #3C4655;
  font-weight: 400;
  @apply bg-[#031840] px-5 py-1 rounded-md grid grid-cols-2;
  @apply justify-items-center
}

.message-block span {
  @apply relative top-[8px] block w-full text-left;
}

.message {
  @apply px-4 py-2 text-[#91969F] rounded-md inline;
  @apply bg-[#3C4655]
}

.actions {
  @apply grid grid-cols-4 justify-items-center w-fit mx-auto;
}

.form-container {
  backdrop-filter: blur(16px);
  background : rgba(0, 0, 0, .5);
  @apply w-screen h-screen fixed z-20;
}

.balance-form {
  margin-top : 20vh;
  @apply w-[350px] rounded-md bg-[#0D2441] mx-auto;
  @apply relative py-6;
}

.balance-input {
  @apply bg-[#3C4655] w-[300px] mx-auto block outline-none;
  @apply py-2 rounded-md border-none pl-3 text-[20px];
}

.save-balance-button {
  @apply bg-[#4D67F0] rounded-md text-center mt-4 w-[300px];
  @apply py-2 mx-auto px-1.5 cursor-pointer;
}

.currency {
  transform : translatex(300px) translateY(4px);
  @apply absolute text-2xl;
}

</style>
