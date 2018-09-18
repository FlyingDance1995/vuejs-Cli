<template>
    <div>
        <p class="title">todos</p>
        <input class="checkAll" @change="changeAll" v-model="changeAllModel" type="checkbox">
        <input type="text" v-on:keyup.enter="addMentor" v-model="mentor">
    </div>
</template>

<script>
export default {
  name: 'Input',
  data(){
      return{
          changeAllModel: false,
          mentor:""
      }
  },
  methods:{
      changeAll(){
          this.$emit("changeAll",this.changeAllModel);
      },
      addMentor(){
          this.$emit("add-item",this.mentor);
          this.mentor= ""
      }
  }
}
</script>

<style scoped>

</style>
