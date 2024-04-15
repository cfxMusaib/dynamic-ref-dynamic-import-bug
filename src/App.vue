<template>
  <keep-alive>
    <comp v-if="currentTab" :ref="currentTab.title" :key="currentTab.title" :title="currentTab.title">
    </comp>
  </keep-alive>
  <button @click="currentTab={title: 'Test1'}">Test1</button>
  <button @click="currentTab={title: 'Test2'}">Test2</button>
  <button @click="currentTab={title: 'Test3'}">Test3</button>
  <button @click="console.log('Refs: ', $refs)">Log Ref</button>
</template>

<script>
import { defineAsyncComponent } from 'vue'
import Comp from './Comp.vue';
export default {
  data: () => ({
    tabs: [{title: "Test1"}, {title: "Test2", something: "es"}, {title: "Test3"}],
    currentTab: {title: "Test1"},
  }),
  components: {Comp:  defineAsyncComponent(() => import('./Comp.vue'))}
}
</script>


Steps to reproduce
1. Click on Test1 button and then click on Log Ref button. Check logs.
2. Now click on Test2 button, then Test 1 button and then click on Log Ref button. Check logs.
3. Do the same after removing the code below
<script setup>
let test;
</script>