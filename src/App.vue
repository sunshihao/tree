<script setup>
	// This starter template is using Vue 3 <script setup> SFCs
	// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
	import {
		reactive,
		ref,
		getCurrentInstance,
		onMounted
	} from "vue";

	// import HelloWorld from './components/HelloWorld.vue'
	// import HiList from './components/HiList.vue'
	// import InfiniteList from 'vue3-infinite-list';
	
	import TreeNode from "./components/TreeNode.vue";
	import DraggableTree from "./components/DraggableTree";

	import data0 from "./table.json";
	import * as hp from "helper-js";
	const data2 = ref([...hp.cloneObject(data0)]);
</script>

<template>
	<!-- <img alt="Vue logo" src="./assets/logo.png" /> -->
	<!-- <HelloWorld msg="Hello Vue 3 + Vite" /> -->
	<!-- <HiList :listData="songs">
	<template #default="{ listItem }">
	    <div>{{ listItem.title }}</div>
	</template>
    </HiList> -->
	<div class="home">
	<DraggableTree v-model="data2" ref="tree3" :defaultOpen="false" dragCopy>
		<!-- <template #default="{ node, stat }"> -->
			<template #default="{ node, stat }">
				
			<a class="home_card">
			<!-- <img class="home_card_tz" style="width: 1em;height: 1em;" src="./assets/tz.svg" />	 -->
			<span v-if="stat.children.length" @click="stat.open = !stat.open">
				{{ stat.open ? "-" : "+" }}
			</span>
			<!-- <img v-if="stat.children.length" @click="stat.open = !stat.open" style="width: 1em;height: 1em;" src="./assets/xia.svg"> -->
			{{ stat.text }}
			</a>
		</template>
	</DraggableTree>
	</div>

</template>

<style scoped>
	
	.home { 
		background-color: azure;
		height: 400px;
		width: 600px;
	}
	
	.home_card { 
		height: 34px;
		font-size: 14px;
	}
	
	.home_card_tz {
		display: none;
	}
	
	.home_card_tz :hover {
		display: block;
	}
	
	#app {
		font-family: Avenir, Helvetica, Arial, sans-serif;
		-webkit-font-smoothing: antialiased;
		-moz-osx-font-smoothing: grayscale;
		text-align: center;
		color: #2c3e50;
		margin-top: 60px;
	}
</style>
