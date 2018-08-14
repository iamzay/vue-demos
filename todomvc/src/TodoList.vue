<template>
  <div>
    <input type="text" v-model="current" @keyup.enter="addTodo(current)">
    <ul class="todo-list">
      <li v-for="(item, index) in filteredTodos" :key="index">
        <div class="view" :class="{completed: item.completed}">
          <input type="checkbox" class="toggle" v-model="item.completed">
          <label @dblclick="edit(index)">{{item.title}}</label>
        </div>
        <div class="edit">
          <input type="text" v-model="item.title" v-todo-focus="index === editIndex"
                 @blur="doneEdit()" @keyup.enter="doneEdit()"
          >
        </div>
      </li>
    </ul>
    <div class="todo-footer">
      <span>{{remains}} items left</span>
      <div>
        <button v-for="(str) in filterArr" :key="str" @click="changeFilter(str)">{{str}}</button>
      </div>
    </div>
  </div>
</template>

<script>
const filters = {
  all: function() {
    return true;
  },
  active: function(item) {
    return !item.completed;
  },
  completed: function(item) {
    return item.completed;
  }
};

export default {
  name: "TodoList",
  props: ["todoList"],
  data: function() {
    return {
      filterStr: "all",
      filterArr: ["all", "active", "completed"],
      current: '',
      editIndex: null
    };
  },
  computed: {
    filteredTodos: function() {
      return this.todoList.filter(filters[this.filterStr]);
    },
    remains: function() {
      return this.todoList.filter(filters.active).length;
    }
  },
  methods: {
    changeFilter: function(str) {
      this.filterStr = str;
    },
    handleItemClick: function(index) {},
    addTodo: function (title) {
      this.todoList.push({ title, completed: false })
      this.current = ''
    },
    edit: function (index) {
      this.editIndex = index
    },
    doneEdit: function () {
      this.editIndex = null
    }
  }
};
</script>

<style>
.completed {
  opacity: 0.5;
  text-decoration: line-through;
}
</style>
