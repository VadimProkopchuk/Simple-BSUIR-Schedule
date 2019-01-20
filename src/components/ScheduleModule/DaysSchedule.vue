<template>
  <b-tabs>
    <b-tab
      v-for="(daySchedule, index) in schedules"
      :key="index"
      :title="getTabTitle(daySchedule)"
      :active="isActiveTab(daySchedule.weekDay)"
    >
      <day-schedule :schedule="daySchedule.schedule" :active-weeks="activeWeeks"></day-schedule>
    </b-tab>
  </b-tabs>
</template>

<script>
import axios from "axios";
import DaySchedule from "./DaySchedule.vue";

export default {
  name: "DaysSchedule",
  components: {
    DaySchedule
  },
  props: {
    schedules: Array,
    activeWeeks: Array
  },
  methods: {
    isActiveTab(weekDay) {
      var now = new Date();
      var weekday = [
        "Воскресенье",
        "Понедельник",
        "Вторник",
        "Среда",
        "Четверг",
        "Пятница",
        "Суббота"
      ];

      return weekDay == weekday[now.getDay()];
    },
    getTabTitle(daySchedule) {
      let weekNumbers = this.activeWeeks
        .filter(x => x.selected)
        .map(x => x.value);
      let countOfLessons = daySchedule.schedule.filter(x =>
        x.weekNumber.some(num => weekNumbers.includes(num))
      ).length;

      return `${daySchedule.weekDay} ${countOfLessons}`;
    }
  }
};
</script>