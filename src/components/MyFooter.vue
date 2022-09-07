<template>
  <div class="todo-footer" v-show="totalCount > 0">
    <label>
      <!-- <input type="checkbox" :checked="checkedAll" @click="doSelect" /> -->
      <input type="checkbox" v-model="checkedAll" />
    </label>
    <span>
      <span>已完成{{ completedCount }}</span> / 全部{{ totalCount }}
    </span>
    <button class="btn btn-danger" @click="doClear">清除已完成任务</button>
  </div>
</template>

<script>
export default {
  name: "MyFooter",
  props: ["todoList", "selectAll", "clearDone"],
  methods: {
    // doSelect(e) {
    //   this.selectAll(e.target.checked);
    // },
    doClear() {
      this.clearDone();
    }
  },
  computed: {
    totalCount() {
      return this.todoList.length;
    },
    completedCount() {
      return this.todoList.filter((e) => e.done).length;
    },
    checkedAll: {
      get() {
        return this.completedCount === this.totalCount && this.totalCount > 0;
      },
      set(value) {
        console.log("checkedAll's set", value);
        this.selectAll(value);
      }
    }
  }
};
</script>

<style scoped>
.todo-footer {
  height: 40px;
  line-height: 40px;
  padding-left: 6px;
  margin-top: 5px;
}
.todo-footer label {
  display: inline-block;
  margin-right: 20px;
  cursor: pointer;
}
.todo-footer label input {
  position: relative;
  top: 1px;
  vertical-align: middle;
  margin-right: 5px;
}
.todo-footer button {
  float: right;
  margin-top: 5px;
}
</style>