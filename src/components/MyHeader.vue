<template>
  <div class="todo-header">
    <input
      type="text"
      placeholder="请输入待办事项"
      class="header"
      @keyup.enter="addTodo"
      v-model="inputTodo"
    />
  </div>
</template>

<script>
import { nanoid } from "nanoid";
export default {
  name: "MyHeader",
  data() {
    return {
      inputTodo: "",
    };
  },
  props: ["getTodo"],
  methods: {
    addTodo() {
      if(!this.inputTodo.trim()) {
        return;
      }
      let newTodo = {
        id: nanoid(),
        title: this.inputTodo,
        done: false,
      };
      this.getTodo(newTodo);
      this.inputTodo = '';
    },
  }
};
</script>

<style scoped>
.todo-header input {
  width: 560px;
  height: 28px;
  font-size: 14px;
  border: 1px solid #ccc;
  border-radius: 4px;
  padding: 4px 7px;
}

.todo-header input:focus {
  outline: none;
  border-color: rgba(82, 168, 236, 0.8);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075),
    0 0 8px rgba(82, 168, 236, 0.6);
}
</style>