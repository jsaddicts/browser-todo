<template>
	<div class="row">
    <div v-bind:class="[showCancel ? 'six columns' : 'nine columns']">
      <input v-on:keyup="onKeyup" class="u-full-width" type="text" placeholder="Add your task" name="task_desc" v-model="value"/>
      <span class="text-danger" v-if="validationErr">{{validationErr}}</span>
    </div>
    <div class="three columns">
      <button class="u-full-width" v-on:click="confirm(value)">{{label}}</button>
    </div>
    <div class="three columns" v-if="showCancel">
      <button class="u-full-width" v-on:click="cancel">Cancel</button>
    </div>
  </div>
</template>

<script>

export default {
  name: 'input-group',
  data () {
    return {
      value : this.defaultValue,
      validationErr: ''
    }
  },
  methods: {
  	clear : function () {
      this.value = "";
    },

  	setErr: function (err) {
      this.validationErr = err;
    },

  	onKeyup: function (e) {
      this.setErr('');
      if(e.key == 'Enter') {
        this.confirm(this.value);
      }
    },

    confirm: function(val) {
    	this.setErr('');

      if(!this.value) {
        this.setErr('Your todo is empty');
        return;
      }

      this.$emit('confirm', val);
      this.clear();
    },

    cancel: function () {
    	this.$emit('cancel')
    }
  },
  props: ['label', 'defaultValue', 'showCancel']
}
</script>