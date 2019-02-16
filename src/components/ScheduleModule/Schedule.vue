<template>
  <div class="p-3">
    <b-form-group class="col-12 col-sm-4 offset-sm-4 col-md-2 offset-md-5">
      <label for="group-number">Enter group number</label>
      <b-form-input v-model="groupNumber" type="text" id="group-number" @change="getGroupScheduler"></b-form-input>
    </b-form-group>
    <h1 class="text-center"
    >{{scheduler ? `Schedule for ${scheduler.studentGroup.name}` : "Loading ..."}}</h1>
    <div v-if="scheduler">
      <subgroup-selector :subgroups="subgroups"></subgroup-selector>
      <week-selector :weeks="activeWeeks"></week-selector>
      <days-schedule :schedules="scheduler.schedules" 
        :active-weeks="activeWeeks" :subgroups="subgroups"></days-schedule>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import DaysSchedule from "./DaysSchedule.vue";
import WeekSelector from "../WeekSelector.vue";
import SubgroupSelector from "../SubgroupSelector.vue";

export default {
  name: "Schedule",
  components: {
    DaysSchedule,
    WeekSelector,
    SubgroupSelector
  },
  data() {
    return {
      groupNumber: 744691,
      scheduler: null,
      activeWeeks: [
        { value: 1, selected: false },
        { value: 2, selected: false },
        { value: 3, selected: false },
        { value: 4, selected: false }
      ],
      endpoint: "https://journal.bsuir.by/api/v1/studentGroup/schedule?studentGroup=",
      subgroups: [
        {value: 0, selected: true },
        {value: 1, selected: true },
        {value: 2, selected: false}
      ]
    };
  },
  created() {
    this.getGroupScheduler();
  },
  methods: {
    getGroupScheduler() {
      this.scheduler = null;
      axios
        .get(this.getEndpointUrl())
        .then(response => {
          this.scheduler = response.data;
          this.activeWeeks.find(
            x => x.value == this.scheduler.currentWeekNumber
          ).selected = true;
        })
        .catch(err => {
          window.console.warn(err);
        });
    },
    getEndpointUrl() {
      return `${this.endpoint}${this.groupNumber}`;
    }
  }
};
</script>