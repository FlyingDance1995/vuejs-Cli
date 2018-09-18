<template>
  <div>
    <span>{{count}} item left </span>
    <button @click="clickAll">All</button>
    <button @click="clickActive">Active</button>
    <button @click="clickCompleted">Completed</button>
    <button @click="clickClear">Clear</button>
  </div>
</template>

<script>
export default {
  name: "Button",
  props: ["index", "todo", "count"],
  data() {
    return {
    };
  },
  methods:{
    clickAll(){
      this.$emit("on-clickAll");
    },
    clickActive(){
      this.$emit("on-clickActive");
    },
    clickCompleted(){
       this.$emit("on-clickCompleted");
    },
    clickClear(){
      this.$emit("on-clickClear");
    }
  }
};
</script>

<style scoped>
</style>
