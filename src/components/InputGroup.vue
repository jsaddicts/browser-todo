<template>
	<div class="row">
    <div class="two-thirds column">
      <input v-on:keyup="onKeyup" class="u-full-width" type="text" placeholder="Add your task" name="task_desc" v-model="value"/>
      <span class="text-danger" v-if="validationErr">{{validationErr}}</span>
    </div>
    <div class="one-third column">
      <button class="u-full-width" v-on:click="onConfirm(value)">{{label}}</button>
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
        this.onConfirm(this.value);
      }
    },

    onConfirm: function(val) {
    	this.setErr('');

      if(!this.value) {
        this.setErr('Your todo is empty');
        return;
      }

      this.$emit('onConfirm', val);
      this.clear();
    }
  },
  props: ['label', 'defaultValue']
}
</script>