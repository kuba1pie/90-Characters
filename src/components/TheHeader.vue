<template>
  <header class="header">
    <div
      class="pageLogo m-6"
      @click="onLogoClick"
    >
      <span class="border-5 border-blue-500/50 font-serif p-3">Messenger</span>
    </div>
    <nav class="nav flex justify-end">
      <TabButton
        v-for="button in buttons"
        :key="button.component"
        :tab-component="button.component"
      >
        {{ button.title }}
      </TabButton>
    </nav>
  </header>
</template>

<script setup lang="ts">
const store = useDefaultStore();

const buttons = [{ "component": "TheEditor", "title": "New message" }, { "component": "TheArchive", "title": "Archive" }]

function onLogoClick() {
  store.changeActiveTab("TheEditor")
}

</script>
<style lang="scss" scope>
.header {
  border-bottom: 2px solid #333c44;
  width: 100vw;

  .nav {
    margin: 0;
  }
}
</style>