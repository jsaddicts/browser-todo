<template>
  <div class="hello">
    <input type="text" placeholder="Add your task" name="task_desc" v-on:change="setTask"/>
    <button v-on:click="addTask(task_desc)">Add</button>
    <ul v-for="task in task_list">
      <li> {{task.text}}</li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'hello',
  data () {
    return {
      task_list : [{
        id : 0,
        text: '',
        completed :false
      }],
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
      },
      setTask : function(e){
        this.task_desc = e.target.value
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
