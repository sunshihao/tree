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

import Draggable from "./Draggable.vue"

import data0 from "./table.json";
import * as hp from "helper-js";
const data2 = ref([...hp.cloneObject(data0), ...hp.cloneObject(data0),
...hp.cloneObject(data0),
...hp.cloneObject(data0),
...hp.cloneObject(data0),
...hp.cloneObject(data0),
...hp.cloneObject(data0),]);
</script>

<template>
	<!-- <img alt="Vue logo" src="./assets/logo.png" /> -->
	<!-- <HelloWorld msg="Hello Vue 3 + Vite" /> -->
	<!-- <HiList :listData="songs">
	<template #default="{ listItem }">
	    <div>{{ listItem.title }}</div>
	</template>
    </HiList> -->
	<!-- <div class="home"> -->
	<!-- 虚拟滚动还是需要高度的 -->
	<DraggableTree v-model="data2" virtualization ref="tree3" style="height: 100vh;width: 300px;" :defaultOpen="true">
		<!-- <template #default="{ node, stat }"> -->
		<template #default="{ node, stat }">
			<a class="home_card">

				<div class="home_card_in">
					<span v-if="stat.children.length" @click="stat.open = !stat.open">
						{{ stat.open ? "-" : "+" }}
					</span>
					{{ node.text }}
				</div>
			</a>
		</template>
	</DraggableTree>
	<!-- </div> -->
	<!-- <div class="home"> -->
	<!-- <Draggable /> -->
	<!-- </div> -->

</template>

<style scoped>
.home {
	background-color: azure;
	height: 400px;
	width: 600px;
	overflow: auto;
}

.home_card {
	margin-top: 2px;
	height: 34px;
	font-size: 14px;
}

.home_card_in {
	border: 1px solid #777;
	border-radius: 4px;
	padding: 4px;
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
