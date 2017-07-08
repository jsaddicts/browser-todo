<template>
  <div class="row margin-top">
    <div class="twelve column">
      <input-group 
        :defaultValue="task_desc"
        label="Add"
        v-on:confirm="addTask"></input-group>
    </div>
    <ul class="task-list">
      <li v-for="task in todoList()">
        <list-item
          :todo="task"
          v-on:save="editTask"
          v-on:remove="removeTask"
          v-on:complete="completeTask"></list-item>
      </li>
    </ul>
    <ul> 
     <li v-for="task in completedList()">
      <del class="text">{{task.text}}</del>
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

    editTask : function(todo){

      this.task_list = this.task_list.map(task => {
        return {
          ...task,
          text: task.id === todo.id ? todo.text : task.text
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
