<template>
  <b-container class="p-3">
    <b-row v-if="hasExistSchedule">
      <b-col
        v-for="(lesson, index) in activeLessons"
        :key="index"
        class="col-12 col-sm-6 col-md-4 col-lg-3"
      >
        <lesson-schedule :lesson="lesson"></lesson-schedule>
      </b-col>
    </b-row>
    <b-row v-else>
      <b-alert variant="success" show>No lessons!</b-alert>
    </b-row>
  </b-container>
</template>

<script>
import LessonSchedule from "./LessonSchedule.vue";

export default {
  name: "DaySchedule",
  components: {
    LessonSchedule
  },
  props: {
    hasExistSchedule: Boolean,
    activeLessons: Array
  }
};
</script>