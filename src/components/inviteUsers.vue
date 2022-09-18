<template>
  <div>
    <div class="search">
      <svg viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg">
        <path d="M12.9 14.32a8 8 0 1 1 1.41-1.41l5.35 5.33-1.42 1.42-5.33-5.34zM8 14A6 6 0 1 0 8 2a6 6 0 0 0 0 12z"/>
      </svg>
      <input
          type="text"
          placeholder="Найти пользователя..."
          v-model="searchValue"/>
    </div>
    <div v-if="isLoading" class="skeleton-list">
      <inviteSkeleton/>
      <inviteSkeleton/>
      <inviteSkeleton/>
    </div>
    <ul v-if="!isLoading" class="users-list">
      <inviteUser
          @onClickInvite="onClickInvite"
          v-for="user in filterUsers()"
          :key="user.id"
          :user="user" :isInvites="invites.includes(user.id)"/>
    </ul>
    <button v-if="invites.length > 0"
        @click="sendInvite"
        class="send-invite-btn"
    >Отправить приглашение</button>
  </div>
</template>

<script>
import inviteSkeleton from './Users/inviteSkeleton.vue'
import inviteUser from './Users/inviteUser.vue'

export default {
  name: "inviteUsers",
  components: {
    inviteSkeleton,
    inviteUser
  },
  props: {
    users: {
      type: Array,
      require: false
    },
    isLoading: {
      type: Boolean,
      require: false
    },
    invites: {
      type: Array,
      require: false
    }
  },
  emits: {
    "nextOnClickInvite": value => typeof value === "number",
    "sendInvite": null,
  },
  data() {
    return {
      searchValue: ""
    }
  },
  methods: {
    filterUsers() {
      return this.users.filter(user => {
            const fullName = (user.first_name + user.last_name).toLowerCase();
            return (
                fullName.includes(this.searchValue.toLowerCase()) ||
                user.email.toLowerCase().includes(this.searchValue.toLowerCase())
            );
          }
      );
    },
    onClickInvite(id) {
      this.$emit("nextOnClickInvite", id);
    },
    sendInvite() {
      this.$emit("sendInvite")
    }
  }
}
</script>

<style scoped>

</style>