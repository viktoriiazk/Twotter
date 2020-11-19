<template>
<div id="app">
{{user.userName}} - {{ fullName }}
<strong>Followers:{{ followers }}</strong>
<button @click="followUser">Follow</button>
</div>
</template>

<script>

export default {
  name: 'App',
  data() {
    return {
      followers: 0,
      user: {
        id: 1,
        userName: '_viktoriiazk',
        firstName: 'Viktoriia',
        lastName: 'Zakorchemna',
        email: 'viktoriia.zakorchemna@gmail.com',
        isAdmin: true
      }
    }
  },
  computed:  {
    fullName() {
return `${this.user.firstName} ${this.user.lastName}`;

    }
    
  },
  methods: {
    followUser() {
      return this.followers++
    }
  },
  mounted() {
    this.followUser();
  }
}
</script>


<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
