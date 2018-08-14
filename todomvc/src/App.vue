<template>
  <div id="app">
    <TodoList :todo-list="todoList"/>
  </div>
</template>

<script>
import TodoList from './TodoList.vue'

export default {
  name: 'app',
  components: {
    TodoList
  },
  data: function () {
    return {
      todoList: [
        { title: 'wash face', completed: false },
        { title: 'play football', completed: false }
      ]
    }
  }
}
</script>

<style>

</style>
