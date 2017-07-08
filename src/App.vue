<template>
  <div class="row">
    <div class="three columns"></div>
    <div class="six columns app-container">
      <div id="app">
        <h1 class="text-center">Browser Todo</h1>
        <todo-list></todo-list>
      </div>
    </div>
    <div class="three columns"></div>
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
  width: 70%;
}

.app-container {
  display: flex;
  justify-content: center;
}

.columns {
  min-height: 1px;
}

@media only screen and (min-width: 678px) and (max-width: 827px) {
  #app {
    width: 85%;
  }
}

@media only screen and (min-width: 550px) and (max-width: 677px) {
  #app {
    width: 95%;
  }
}

@media only screen and (max-width: 549px) {
  #app {
    width: 100%;
  }
}
</style>
