<template>
  <div id="app">
    <schedule/>
  </div>
</template>

<script>
import Schedule from "./components/ScheduleModule/Schedule.vue";

export default {
  name: "app",
  components: {
    Schedule
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
