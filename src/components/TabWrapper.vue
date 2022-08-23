<template>
  <div v-if="store.activeTab === 'TheArchive'">
    <TheArchive />
  </div>
  <div v-else>
    <TheEditor />
  </div>
</template>
<script setup lang="ts">
const store = useDefaultStore();
</script>