<template>
  <b-card
    :title="getLessonTitle(lesson)"
    :sub-title="getAuditory(lesson)"
    :class="['mb-3', 'border-3', `border-${getBorderColor(lesson.lessonType)}`]"
  >
    <b-alert show variant="warning" v-if="lesson.note">{{lesson.note}}</b-alert>
    <p class="card-text text-danger">
      <strong>{{lesson.lessonTime}}</strong> {{getSubgroup(lesson)}}
    <div class="card-body text-center" v-for="employer in lesson.employee" 
      :key="employer.id">
      <img :src="employer.photoLink" class="" width="120">
      <p class="card-text">{{employer.fio}}</p>
    </div>
  </b-card>
</template>


<script>
export default {
  name: "LessonSchedule",
  props: {
    lesson: Object
  },
  methods: {
    getLessonTitle(lesson) {
      return `${lesson.subject} (${lesson.lessonType})`;
    },
    getAuditory(lesson) {
      return lesson.auditory.join(",");
    },
    getSubgroup(lesson){
      const subGroup = lesson.numSubgroup;
      if (subGroup != 0) {
        return `${subGroup} (п.)`;
      }
    },
    getBorderColor(lessonType) {
      switch (lessonType) {
        case "ЛР":
          return "danger";
        case "ПЗ":
          return "warning";
        default:
          return "success";
      }
    }
  }
};
</script>

<style scoped>
.border-3 {
  border-width: 3px;
}
</style>
