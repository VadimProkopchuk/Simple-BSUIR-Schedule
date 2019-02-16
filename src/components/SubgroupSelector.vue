<template>
  <div>
    <h5>Sub-Groups</h5>
    <b-form-checkbox v-for="subgroup in getAvailableSubgroups()" 
      :key="subgroup.value" 
      v-model="subgroup.selected">{{subgroup.value}}</b-form-checkbox>
  </div>
</template>

<script>
export default {
  name: "SubgroupSelector",
  props: {
    subgroups: Array
  },
  methods:{
    getAvailableSubgroups(){
      return this.subgroups.filter(x => x.value > 0);
    }
  }
};
</script>