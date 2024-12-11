<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <ReportPage/>
</template>

<script>
import ReportPage from "@/components/ReportPage.vue";

export default {
  name: 'App',
  components: {
    ReportPage,
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
}
</style>
