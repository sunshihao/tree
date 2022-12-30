<template>
    <table v-if="table">
        <slot name="prepend"></slot>
        <tbody>
            <slot></slot>
        </tbody>
        <slot name="append"></slot>
    </table>
    <div v-else>
        <slot name="prepend"></slot>
        <slot></slot>
        <slot name="append"></slot>
    </div>
</template>
  
<script lang="ts" setup>
//   import { defineComponent } from "vue-demi"; // 对于工程我们只做vue3的适配性工作
import { defineProps, toRefs } from "vue"

const props = defineProps({
    table: Boolean
})

const { table } = toRefs(props)

//   export default defineComponent({
//     props: {
//       table: Boolean,
//     },
//   });
</script>