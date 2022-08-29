<template>
  <button
    class="c-tabButton rounded-2 rounded-2xl border-blue-500/50 bg-blue-500/50 p-2 m-2"
    :class="{ active: isActive }"
    @click="onTabClick"
  >
    <slot />
  </button>
</template>

<script setup lang="ts">

const store = useDefaultStore();
const props = defineProps<{
  tabComponent: string
}>()
const isActive = computed(() => {
  return (store.activeTab === props.tabComponent)
})

function onTabClick() {
  store.changeActiveTab(props.tabComponent)
}
</script>
