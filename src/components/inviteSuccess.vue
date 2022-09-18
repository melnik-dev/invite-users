<template>
  <div class="success-block">
    <img src="../assets/success.svg" alt="Success" />
    <h3>Успешно!</h3>
    <p>Всем {{ count }} пользователям отправлено приглашение.</p>
    <button @click="reloadPage" class="send-invite-btn">Назад</button>
  </div>
</template>

<script>
export default {
  name: "inviteSuccess",
  props: {
    count: {
      type: Number,
      require: true
    }
  },
  methods: {
    reloadPage() {
      window.location.reload()
    }
  }
}
</script>

<style scoped>

</style>