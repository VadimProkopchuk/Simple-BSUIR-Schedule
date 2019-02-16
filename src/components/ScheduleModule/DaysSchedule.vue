<template>
  <b-tabs>
    <b-tab
      v-for="(daySchedule, index) in schedules"
      :key="index"
      :title="getTabTitle(daySchedule)"
      :active="isActiveTab(daySchedule.weekDay)">
      <day-schedule :has-exist-schedule="daySchedule.schedule !== null" 
        :active-lessons="getActiveLessons(daySchedule)"></day-schedule>
    </b-tab>
  </b-tabs>
</template>

<script>
import DaySchedule from "./DaySchedule.vue";

export default {
  name: "DaysSchedule",
  components: {
    DaySchedule
  },
  props: {
    schedules: Array,
    activeWeeks: Array,
    subgroups: Array
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
      return `${daySchedule.weekDay} ${this.getActiveLessons(daySchedule).length}`;
    },
    getActiveLessons(daySchedule) {
      if (daySchedule.schedule){
        let weekNumbers = this.activeWeeks.filter(x => x.selected).map(x => x.value);
        let activeSubgroups = this.subgroups.filter(x => x.selected).map(x => x.value);

        return daySchedule.schedule.filter(x => x.weekNumber.some(num => weekNumbers.includes(num)) && activeSubgroups.includes(x.numSubgroup));
      }

      return [];
    }
  }
};
</script>