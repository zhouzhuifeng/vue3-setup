<template>
	<img alt="Vue logo" src="./assets/logo.png" />
	<HelloWorld msg="Hello Vue 3 + Vite" />
	<Child :isParent="childMsg" @toParent="toParent"></Child>
</template>

<script setup>
import HelloWorld from './components/HelloWorld.vue';
import Child from './components/child.vue';
import { ref } from 'vue';
const childMsg = ref('父组件传过来的');
const toParent = (val) => {
	childMsg.value = val;
};
// This starter template is using Vue 3 experimental <script setup> SFCs
// Check out https://github.com/vuejs/rfcs/blob/script-setup-2/active-rfcs/0000-script-setup.md
</script>

<style>
#app {
	font-family: Avenir, Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;
	color: #2c3e50;
	margin-top: 60px;
}
</style>
