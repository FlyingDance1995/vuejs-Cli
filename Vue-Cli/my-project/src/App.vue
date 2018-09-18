<template>
  <div id="app">
    <Input @add-item="getMentorFromChild" @changeAll="changeAllStatus" />
    <ol>
        <TodoItem :todo="item" :key="item.id" :index= "index" v-for="(item, index) in copyTodos" @on-change="updateItem"></TodoItem>
    </ol>
    <Button :count= "count" @on-clickAll="ClickAll" @on-clickActive="ClickActive" @on-clickCompleted="ClickCompleted" @on-clickClear= "ClickClear"/>
  </div>
</template>

<script>
import Input from "./components/Input.vue";
import TodoItem from "./components/TodoItem.vue";
import Button from "./components/Button.vue";

export default {
  name: "app",
  components: {
    Input,
    TodoItem,
    Button
  },
  data() {
    return {
      temp: "all",
      todos: []
    };
  },
  computed: {
    copyTodos() {
      if (this.temp == "all") {
        return this.todos;
      }
      if (this.temp == "active") {
        let temp = this.todos.filter(function(todo) {
          return !todo.status;
        });
        return temp;
      }
      if (this.temp == "completed") {
        return this.todos.filter(function(todo) {
          return todo.status;
        });
      }
    },

    count: function() {
      let c = 0;
      this.todos.forEach(element => {
        if (element.status == false) c++;
      });
      return c;
    }
  },
  methods: {
    changeAllStatus(value) {
      if (value) {
        this.todos.forEach(element => {
          element.status = true;
        });
      } else {
        this.todos.forEach(element => {
          element.status = false;
        });
      }
    },
    getMentorFromChild(value) {
      if (value != "") {
        this.todos.push({
          todo: value,
          status: false
        });
      }
    },

    updateItem(actionType, newValue) {
      if (actionType === "changeStatus") {
        let { index, status } = newValue;
        // TODO:
        this.todos[index].status = status;
      }
      if (actionType === "editContent") {
        let { index, content } = newValue;
        // TODO:
        this.todos[index].todo = content;
      }
      if (actionType === "removeItem") {
        let { index } = newValue;
        // TODO:
        this.todos.splice(index, 1);
      }
    },
    ClickAll() {
      this.temp = "all";
    },
    ClickActive() {
      this.temp = "active";
    },
    ClickCompleted() {
      this.temp = "completed";
    },
    ClickClear() {
      this.todos = this.todos.filter(function(todo) {
        return !todo.status;
      });
    }
  }
};
</script>

<style>
</style>
