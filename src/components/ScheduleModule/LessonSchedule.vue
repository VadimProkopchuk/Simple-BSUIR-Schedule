<template>
  <b-card
    :title="getLessonTitle(lesson)"
    :sub-title="getAuditory(lesson)"
    :class="['mb-3', 'border-3', `border-${getBorderColor(lesson.lessonType)}`]"
  >
    <b-alert show variant="warning" v-if="lesson.note">{{lesson.note}}</b-alert>
    <p class="card-text text-danger">{{lesson.lessonTime}}</p>
    <p class="card-text">{{getEmployes(lesson)}}</p>
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
    getEmployes(lesson) {
      return lesson.employee.map(x => x.fio).join(", ");
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
