<template>
  <div>
    <div v-if="!edit">
      <input class="todo-list-item" type="checkbox" v-bind:checked="editabletodo.completed" v-on:change="complete(editabletodo.id)"/>
      {{editabletodo.text}}
      <span v-on:click="enableEdit()" class="text-primary pointer">Edit</span>
    </div>
    <div v-if="edit">
    	<input-group 
        label="Save"
        :defaultValue="editabletodo.text"
        :showCancel="true"
        v-on:cancel="disableEdit"
        v-on:confirm="onConfirm"></input-group>
    </div>
  </div>
</template>

<script>
import InputGroup from './InputGroup';

export default {
  name: 'list-item',
  components: {
    InputGroup
  },
  data () {
    return {
      editabletodo : this.todo,
      edit: false
    }
  },
  watch: {
		todo: function (val, oldVal) {
			this.editabletodo = val;
		},
	},
  methods: {
    save: function(val) {
      this.$emit('save', val)
    },
    complete: function(id) {
    	this.$emit('complete', id)
    },
    enableEdit: function() {
      this.edit = true;
    },
    onConfirm: function (val) {
    	this.save({
      	...this.editabletodo,
      	text: val
      })
     	this.disableEdit();
    },
    disableEdit: function() {
      this.edit = false;
    }
  },
  props: ['todo']
}
</script>
