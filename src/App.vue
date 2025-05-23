<template>
  <div id="app">
    <FormUser @updateUser="updateUser" />
    <div class="cards-row">
      <UserCard
        :user="user"
        :fixedColor="'#ECB117'"
      />
      <UserCard
        :user="user"
        :fixedColor="'#9B0021'"
      />
    </div>
  </div>
</template>

<script>
import UserCard from './components/UserCard.vue';
import FormUser from './components/FormUser.vue';

export default {
  name: 'App',
  components: {
    FormUser,
    UserCard
  },
  data() {
    return {
      user: {
        photo: '',
        name: '',
        surname: '',
        cardColor: '#ECB117'
      },
      emptyUser: {
        photo: '',
        name: '',
        surname: '',
        cardColor: ''
      }
    };
  },
  methods: {
    updateUser(userData) {
      this.user = { ...this.user, ...userData };
    }
  }
}
</script>

<style>
#app {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: flex-start;
  min-height: 100vh;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  color: #2c3e50;
  margin-top: 40px;
}
.cards-row {
  display: flex;
  gap: 40px;
  margin-top: 32px;
}
/* No seu App.vue */
.cards-row {
  display: flex;
  gap: 40px;
  margin-top: 32px;
}

@media (max-width: 600px) {
  .cards-row {
    flex-direction: column;
    gap: 24px;
    align-items: center;
  }
}
</style>