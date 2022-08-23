<template>
  <button
    class="c-tabButton rounded-none rounded-2xl"
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
