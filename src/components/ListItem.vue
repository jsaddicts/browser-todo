<template>
  <div>
    <div v-if="!edit">
      <input class="todo-list-item" type="checkbox" v-bind:checked="editabletodo.completed" v-on:change="completeTask(editabletodo.id)"/>
      {{editabletodo.text}}
      <span v-on:click="enableEdit()">Edit</span>
    </div>
    <div v-if="edit">
      <input type="text" v-model="editabletodo.text">
      <span v-on:click="disableEdit">Save</span>
    </div>
  </div>
</template>

<script>

export default {
  name: 'list-item',
  data () {
    return {
      editabletodo : this.todo,
      edit: false
    }
  },
  methods: {
    onSave: function(val) {
      this.$emit('onSave', val)
    },
    enableEdit: function() {
      this.edit = true;
    },
    disableEdit: function() {
      this.edit = false;
      this.onSave(this.editabletodo)
    }
  },
  props: ['todo']
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
