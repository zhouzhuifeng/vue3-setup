<template>
	<div>
		<h4>{{ isParent }}</h4>
		<button @click="toEmit">emit to parent</button>
	</div>
</template>

<script setup>
import { defineProps, useContext } from 'vue';
const { slots, attrs,emit } = useContext();
defineProps({
	isParent: '',
});
defineEmit(['toParent']);
const toEmit = () => {
	emit('toParent', '我是子组件传过来的');
};
</script>

<style lang="scss" scoped></style>
