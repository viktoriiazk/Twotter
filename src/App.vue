<template>
<div id="app">
<UserProfile/>
</div>
</template>

<script>
import UserProfile from "./components/UserProfile";
export default {
name: 'App',
components: { UserProfile }
}
</script>


<style>
body {
  background-color: #c5cbc5;
}
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
  width: 100vw;
}
</style>
