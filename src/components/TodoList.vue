<template>
  <div class="row margin-top">
    <div class="twelve column">
      <div class="row">
        <div class="two-thirds column">
          <input class="u-full-width" type="text" placeholder="Add your task" name="task_desc" v-model="task_desc"/>
        </div>
        <div class="one-third column">
          <button class="u-full-width" v-on:click="addTask(task_desc)">Add</button>
        </div>
      </div>
    </div>
    <ul v-for="task in todoList()">
      <li>
        <input type="checkbox" v-bind:checked="task.completed" v-on:change="completeTask(task.id)"/>
        {{task.text}}
      </li>
    </ul>
    <ul v-for="task in completedList()"> 
     <li v-on:click="removeTask(task.id)">
      <del>{{task.text}}</del>
     </li> 
    </ul>
  </div>
</template>

<script>
export default {
  name: 'todo-list',
  data () {
    return {
      task_list : [],
      task_desc :''
    }
  },

  methods: {

    addTask : function(text){
      this.task_list.push({
        id : Date.now(),
        text : text,
        completed : false
      })
      this.clear()
    },

    completeTask : function(id){

      this.task_list = this.task_list.map(task => {
        return {
          ...task,
          completed: task.id === id ? true : task.completed
        }
      })

    },

    clear : function(){
      this.task_desc = ""
    },

    removeTask : function(id){
      var task_list = this.task_list.filter(function(task){
        if(task.id != id ){
          return task
        }
      })
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

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
