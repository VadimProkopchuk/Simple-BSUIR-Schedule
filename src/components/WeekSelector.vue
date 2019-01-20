<template>
  <div>
    <h5>Weeks</h5>
    <b-form-checkbox v-for="week in weeks" :key="week.value" v-model="week.selected">{{week.value}}</b-form-checkbox>
  </div>
</template>

<script>
export default {
  name: "WeekSelector",
  props: {
    weeks: Array
  }
};
</script>