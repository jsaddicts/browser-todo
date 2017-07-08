<template>
  <div class="row margin-top">
    <div class="twelve column">
      <input-group 
        :value="task_desc"
        label="Add"
        v-on:onConfirm="addTask"></input-group>
    </div>
    <ul class="task-list">
      <li v-for="task in todoList()">
        <list-item :todo="task"></list-item>
      </li>
    </ul>
    <ul> 
     <li v-for="task in completedList()">
      <del>{{task.text}}</del>
      <span class="text-danger pointer" v-on:click="removeTask(task.id)">delete</span>
     </li> 
    </ul>
  </div>
</template>

<script>

import ListItem from './ListItem';
import InputGroup from './InputGroup';

function getList () {
  return JSON.parse(localStorage.getItem('BrowserTodoList')) || [];
}

function saveList (list) {
  return localStorage.setItem('BrowserTodoList', JSON.stringify(list));
}

export default {
  name: 'todo-list',
  components: {
    ListItem,
    InputGroup
  },
  data () {
    return {
      task_list : [],
      task_desc :'',
      validationErr: ''
    }
  },

  created: function () {
    if(window.localStorage) {
      this.task_list = getList();
    }
  },

  watch: {
    task_list: function(newList) {
      saveList(newList);
    }
  },

  methods: {

    addTask : function(val){
    
      this.task_list.push({
        id : Date.now(),
        text : val,
        completed : false
      })

    },

    completeTask : function(id){

      this.task_list = this.task_list.map(task => {
        return {
          ...task,
          completed: task.id === id ? true : task.completed
        }
      })

    },

    removeTask : function(id){
      this.task_list = this.task_list.filter(task => task.id !== id)
    },

    completedList: function () {
      return this.task_list.filter(task => task.completed === true);
    },

    todoList: function () {
      return this.task_list.filter(task => task.completed === false);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

a {
  color: #42b983;
}
</style>
