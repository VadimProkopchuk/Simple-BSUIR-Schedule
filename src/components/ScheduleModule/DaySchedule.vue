<template>
  <b-container class="p-3">
    <b-row v-if="schedule">
      <b-col
        v-for="(lesson, index) in getActiveLessons()"
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
    schedule: Array,
    activeWeeks: Array
  },
  methods: {
    getActiveLessons() {
      let weekNumbers = this.activeWeeks
        .filter(x => x.selected)
        .map(x => x.value);
      return this.schedule.filter(x =>
        x.weekNumber.some(num => weekNumbers.includes(num))
      );
    }
  }
};
</script>