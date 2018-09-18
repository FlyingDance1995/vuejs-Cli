<template>
    <li>
        <input class="checkboxItem" type="checkbox" v-model="data.status" @change="changeStatus">
        <label v-bind:style="[data.status ? { 'textDecoration':'line-through','color':'red'}:{'textDecoration':'none','color':'blue'}]"
            @dblclick="editTodoChild(data.todo)">{{data.todo}}</label>
        <img @click="removeItemChild(index)" src="../assets/icons/removeItem.jpg" width="20px" height="15px">
    </li>
</template>

<script>
export default {
  name: "TodoItem",
  props: ["index", "todo"],
  data() {
    return {
      data: this.todo
    };
  },
  watch: {
    todo() {
      this.data = this.todo;
    }
  },
  methods: {
    changeStatus() {
      this.$emit("on-change", "changeStatus", {
        index: this.index,
        status: this.data.status
      });
    },
    editTodoChild() {
      this.$emit("on-change", "editContent", {
        index: this.index,
        content: this.data.content
      });
    },
    removeItemChild(index) {
      this.$emit("on-change", "removeItem", {
        index: this.index
      });
    }
  }
};
</script>

<style scoped>
.checkboxItem {
  margin-left: -150px;
  margin-right: -100px;
}
img {
  width: 15px;
  margin-left: 20px;
}
input {
  width: 290px;
}
li{
  list-style: none;
}
</style>
