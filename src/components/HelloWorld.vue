<template>
	<h1>{{ msg }}</h1>

	<p>
		<a href="https://vitejs.dev/guide/features.html" target="_blank"
			>Vite Documentation</a
		>
		|
		<a href="https://v3.vuejs.org/" target="_blank">Vue 3 Documentation</a>
	</p>

	<button @click="addCount">count is: {{ state.count }}</button>
	<div :style="{ marginTop: '20px' }" class="isFlex">
		<button @click="btnClick">变色</button>
		<div>
			<div
				v-for="(item, i) in list"
				:ref="
					(el) => {
						if (el) divs[i] = el;
					}
				"
				:key="item"
			>
				{{ item }}
			</div>
		</div>
	</div>
	<div class="mt20 isFlex">
		<button @click="setName">触发watch</button>
		<div>
			<div>firstName:{{ firstName }}</div>
			<div>lastName: {{ lastName }}</div>
		</div>
	</div>
</template>
<script setup>
import {
	reactive,
	ref,
	watch,
	watchEffect,
	onMounted,
	onBeforeUpdate,
	toRefs,
	defineProps,
	defineEmit,
	useContext,
} from 'vue';
const props = defineProps({
	msg: String,
});
// 单个值用ref，ref的取值一定用.value
let count = ref(0);
// 对象用reactive，多值的情况
const state = reactive({ count: 0 });

const btnClick = () => {
	list.push('改变了');
	divs.value[0].style.color = 'red';
};

const firstName = ref('');
const lastName = ref('');

watch([firstName, lastName, () => state.count], (newValues, prevValues) => {
	console.log(newValues, prevValues);
});

const setName = () => {
	firstName.value = 'John'; // logs: ["John",""] ["", ""]
	lastName.value = 'Smith'; // logs: ["John", "Smith"] ["John", ""]
};

onMounted(() => {
	// DOM元素将在初始渲染后分配给ref
	console.log('onMounted这是根元素'); // <div>这是根元素</div>
});

watchEffect(() =>
	console.log(
		count.value,
		'组件初始化的时候就会执行watchEffect，响应式属性改变时都会执行',
		'count.value'
	)
);
const list = reactive([1, 2, 3]);
const divs = ref([]);
function addCount() {
	state.count += 1;
}

// 确保在每次更新之前重置ref
onBeforeUpdate(() => {
	console.log(divs.value, '3333');
	divs.value = [];
	console.log(divs.value, '4444');
});
</script>

<style scoped>
a {
	color: #42b983;
}
.mt20 {
	margin-top: 20px;
}
.isFlex {
	display: flex;
	justify-content: center;
	align-items: center;
}
button {
	margin-right: 20px;
}
</style>
