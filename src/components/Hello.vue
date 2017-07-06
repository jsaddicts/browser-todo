<template>
  <div class="hello">
    <input type="text" placeholder="Add your task" name="task_desc" v-model="task_desc"/>
    <button v-on:click="addTask(task_desc)">Add</button>
    <ul v-for="task in task_list">
      <li v-on:click="completeTask(task)">
        <input type="checkbox" v-model="task.completed"/>
        {{task.text}}
      </li>
      </ul>
     <ul v-for="task in task_list" v-if="task.completed"> 
     <li v-on:click="removeTask(task.id)">
      <del>{{task.text}}</del>
     </li> 
    </ul>
  </div>
</template>

<script>
export default {
  name: 'hello',
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
          completed : this.completed
        })
        this.clear()
      },
      completeTask : function(task){
        task.completed = true 
      },
      clear : function(){
        this.task_desc = ""
      },
      removeTask : function(id){
        console.log(this.task_list)
        var task_list = this.task_list.filter(function(task){
          console.log(task)
            if(task.id != id ){
              return task
            }
        })
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
