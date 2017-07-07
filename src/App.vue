<template>
  <div class="row">
    <div class="one-third column"></div>
    <div class="one-third column">
      <div id="app">
        <h1 class="text-center">Browser Todo</h1>
        <todo-list></todo-list>
      </div>
    </div>
    <div class="one-third column"></div>
  </div>
</template>

<script>
import TodoList from './components/TodoList'
import './style/common.css'

export default {
  name: 'app',
  components: {
    TodoList
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}

.column {
  min-height: 1px;
}
</style>
