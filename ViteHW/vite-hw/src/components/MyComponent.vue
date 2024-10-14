<script>

import { ref, onMounted } from 'vue';

export default {
	setup() {
		// Ref is like reactive, but just a single value instead of an object.
		const name = ref('');
		
		const submitForm = () => {
			// Only works with these quotes
			console.log(`Form submitted = ${name.value}`);
		}
		
		const el = ref()
		
		// Lifecycle hook
		onMounted(() => {
			// Template ref
			el.value.focus();
		})
		
		// To make data available to template, it has to be returned by setup.
		return {
			name,
			submitForm,
			el
		}
	},
}
</script>

<template>
  <div>
  	<p>{{ name }}</p>
  	<!-- v-model makes 2-way data binding with name -->
    <input ref="el" type="text" placeholder="Name" v-model="name"/>
    <input type="text" placeholder="Name2" v-model="name"/>
    <div>
    	<!-- v-on:click can be written as @click -->
    	<button 
    		@click="submitForm"
    		v-bind:disabled="name.length == 0">
    	Submit</button>
    </div>
  </div>
</template>

<style>
input[type='text'] {
	padding: 5px;
}
button {
	margin-top: 20px;
}
</style>
