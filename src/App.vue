<template>
  <div id="app">
    <div class="todo-container">
      <div class="todo-wrap">
        <MyHeader :getTodo="getTodo"></MyHeader>
        <MyList
          :todoList="todoList"
          :selectOne="selectOne"
          :deleteOne="deleteOne"
        ></MyList>
        <MyFooter
          :todoList="todoList"
          :selectAll="selectAll"
          :clearDone="clearDone"
        ></MyFooter>
      </div>
    </div>
  </div>
</template>

<script>
import MyHeader from "./components/MyHeader.vue";
import MyList from "./components/MyList.vue";
import MyFooter from "./components/MyFooter.vue";

export default {
  name: "App",
  components: {
    MyHeader,
    MyList,
    MyFooter,
  },
  data() {
    return {
      todoList: [
        { id: "1001", title: "抽烟", done: false },
        { id: "1002", title: "喝酒", done: false },
        { id: "1003", title: "烫头", done: true },
        { id: "1004", title: "写代码", done: true },
      ],
    };
  },
  methods: {
    getTodo(e) {
      this.todoList.unshift(e);
    },
    selectAll(checked) {
      console.log("this is App's selectAll", checked);
      this.todoList.forEach((e) => (e.done = checked));
    },
    selectOne(id) {
      this.todoList.forEach((e) => {
        if (e.id === id) {
          console.log("this is App's selectOne", id);
          e.done = !e.done;
        }
      });
    },
    deleteOne(id) {
      console.log("this is App's deleteOne", id);
      this.todoList = this.todoList.filter((e) => e.id !== id);
    },
    clearDone() {
      console.log("this is App's deleteOne");
      this.todoList = this.todoList.filter((e) => e.done !== true);
    },
  },
  computed: {
    completedCount() {
      return this.todoList.filter((t) => t.done).length;
    },
    totalCount() {
      return this.todoList.length;
    },
  },
};
</script>

<style>
body {
  background-color: #fff;
}
.btn {
  display: inline-block;
  padding: 4px 12px;
  margin-bottom: 0;
  font-size: 14px;
  line-height: 20px;
  text-align: center;
  vertical-align: middle;
  cursor: pointer;
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2),
    0 1px 2px rgba(0, 0, 0, 0.05);
  border-radius: 4px;
}
.btn-danger {
  color: #fff;
  background-color: #da4f49;
  border: 1px solid #bd362f;
}
.btn-danger:hover {
  color: #fff;
  border: 1px solid #bd362f;
}
.btn:focus {
  outline: none;
}
.todo-container {
  width: 600px;
  margin: 0 auto;
}
.todo-container .toto-wrap {
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 5px;
}
</style>
