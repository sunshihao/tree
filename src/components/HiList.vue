<template>
  <ul ref="ulRef">
    <li v-for="(listItem, listIndex) in listData" :key="`list-${listIndex}`" :data-idx="listItem.idx">
      <slot :listItem="listItem"></slot>
    </li>
  </ul>
</template>


<script lang="ts" setup>
/** 终究还是要 */
import { ref, computed, nextTick, reactive, watchEffect, onUnmounted } from 'vue'

/** 进行参数的接收 */ 
const props = defineProps<{
  listData: Array<any>
}>()

// 列表HTMLElementDom
const ulRef = ref<any>(null)

// 屏幕高度
const screenH = document.documentElement.clientHeight

console.log('screenHscreenH', screenH)

const data = reactive<any>({
  // 列表第一项的高度（起始高度）
  initH: 0,

  // 一行的高度
  unitH: 0,

  // 屏幕范围内能显示个数
  displayCount: 1,

  // 列表起始值
  startIdx: 0
})

const listData = computed(() => {
  let endIdx = data.startIdx + data.displayCount
  if (endIdx >= props.listData.length) endIdx = props.listData.length

  // 通过这个来进行操作
  return props.listData.slice(data.startIdx, endIdx).map((v, k) => {
    v.idx = data.startIdx + k + 1
    return v
  })
})

function scrollHandler() {

  console.log('scrollHandlerscrollHandlerscrollHandler')	
  // 当前滚动高度
  const curScrollTop = document.documentElement.scrollTop
  // 获取滚动条位置
  
  console.log('datadatadata', data)
  
  if (curScrollTop > data.initH) {
    const addCount = Math.floor((curScrollTop - data.initH) / data.unitH)
    ulRef.value.style.setProperty('padding-top', `${addCount * data.unitH}px`)
    data.startIdx = addCount
  } else {
    ulRef.value.style.setProperty('padding-top', '0px')
    data.startIdx = 0
  }
}

watchEffect(() => {
  if (props.listData.length > 0) {
    nextTick(() => {
	  //
      // 列表距离顶部距离 计算有问题没算定自己的高度
	  console.log('ulRef.value.getBoundingClientRect()', ulRef.value.getBoundingClientRect())
      data.initH = ulRef.value.getBoundingClientRect().top + document.documentElement.scrollTop
      // 返回的是矩形的集合
      // 表示了当前盒子在浏览器中的位置以及自身占据的空间的大小，除了 width 和 height 之外
      // 其他的属性是相对于视图窗口的左上角 来计算的
	  // 放大镜和拖拽就是利用这个属性方法来完成了定位
	  
	  // 计算每行高度
      data.unitH = ulRef.value.children[0].offsetHeight
      // 计算屏幕内能显示的行数
	  // 显示的区域高度应为窗体的区域高度 - 滚动区域
      data.displayCount = Math.ceil((screenH - ulRef.value.getBoundingClientRect().top) / data.unitH)
      // 设置列表总高度 = 一行高度 * 行数
      const listH = data.unitH * props.listData.length
      ulRef.value.style.setProperty('height', `${listH}px`)

      window.removeEventListener('scroll', scrollHandler)
      window.addEventListener('scroll', scrollHandler)
    })
  }
})

onUnmounted(() => {
  window.removeEventListener('scroll', scrollHandler)
})
</script>

