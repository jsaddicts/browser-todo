<template>
  <div class="row margin-top">
    <div class="twelve column">
      <div class="row">
        <div class="two-thirds column">
          <input v-on:keyup="onKeyup" class="u-full-width" type="text" placeholder="Add your task" name="task_desc" v-model="task_desc"/>
          <span class="text-danger" v-if="validationErr">{{validationErr}}</span>
        </div>
        <div class="one-third column">
          <button class="u-full-width" v-on:click="addTask">Add</button>
        </div>
      </div>
    </div>
    <ul class="task-list">
      <li v-for="task in todoList()">
        <input class="task-list-item" type="checkbox" v-bind:checked="task.completed" v-on:change="completeTask(task.id)"/>
        {{task.text}}
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
export default {
  name: 'todo-list',
  data () {
    return {
      task_list : [],
      task_desc :'',
      validationErr: ''
    }
  },

  methods: {

    setErr: function (err) {
      this.validationErr = err;
    },

    addTask : function(){
      this.setErr('');

      if(!this.task_desc) {
        this.setErr('Please write a task');
        return;
      }

      this.task_list.push({
        id : Date.now(),
        text : this.task_desc,
        completed : false
      })

      this.clear();  // clear the input box

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
      this.task_desc = "";
    },

    removeTask : function(id){
      this.task_list = this.task_list.filter(task => task.id !== id)
    },

    completedList: function () {
      return this.task_list.filter(task => task.completed === true);
    },

    todoList: function () {
      return this.task_list.filter(task => task.completed === false);
    },

    onKeyup: function (e) {
      if(e.key == 'Enter') {
        this.addTask();
      }
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
