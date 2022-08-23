<template>
  <header class="c-theHeader">
    <div class="header">
      <div
        class="pageLogo"
        @click="onLogoClick"
      >
        <img src="../assets/vue.svg">
      </div>
      <nav class="nav">
        <TabButton
          v-for="button in buttons"
          :key="button.component"
          :tab-component="button.component"
        >
          {{ button.title }}
        </TabButton>
      </nav>
    </div>
    <div class="header-bar" />
  </header>
</template>

<script setup lang="ts">
const store = useDefaultStore();

const buttons = [{ "component": "TheEditor", "title": "New message" }, { "component": "TheArchive", "title": "Archive" }]

function onLogoClick() {
  store.changeActiveTab("TheEditor")
}

</script>
