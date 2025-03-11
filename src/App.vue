<script setup>
import { computed, ref } from 'vue'

import Flicking from '@egjs/vue3-flicking'
import { Pagination, Arrow } from '@egjs/flicking-plugins'
import('@egjs/vue3-flicking/dist/flicking.css')
import('@egjs/flicking-plugins/dist/flicking-plugins.css')

const options = computed(() => {
  return {
    align: 'prev',
    bound: true,
    preventDefaultOnDrag: true,
    resizeOnContentsReady: true
  }
})

const moveCount = ref(Math.random() < 0.5 ? 1 : 2)

const plugins = computed(() => {
  return [
    new Pagination(),
    new Arrow({
      moveCount: moveCount.value
    })
  ]
})
</script>

<template>
  <button @click="moveCount = Math.max(1, (moveCount + 1) % 3)">Switch move count: {{ moveCount }}</button>
  <Flicking :options="options" :plugins="plugins">
    <div
      v-for="i in 10"
      :key="i"
      class="plugins-panel"
    >
      <img class="panel-image" src="https://picsum.photos/200/300" />
    </div>
    <template #viewport>
      <div class="flicking-pagination"></div>
      <span class="flicking-arrow-prev"></span>
      <span class="flicking-arrow-next"></span>
    </template>
  </Flicking>
</template>

<style>
</style>
