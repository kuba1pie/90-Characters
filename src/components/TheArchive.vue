<template>
  <div class="c-theArchive">
    <h2>Message history</h2>
    <MessageContent
      v-for="item in store.archiveMessages"
      :key="item"
      class="border-red-500/50"
      :message-data="item"
    />
  </div>
</template>
<script setup lang="ts">import { Message } from '../types';

const store = useDefaultStore();


function getLocalStorage() {
  let archiveData: Message[] = [];
  if (window.localStorage.getItem('archiveData') !== "") {
    try {
      archiveData = JSON.parse(localStorage.getItem('archiveData')!) as Message[];
      store.setArchive(archiveData)
    } catch (e) {
      return;
    }
  }
  else {
    archiveData = []
  }
}

getLocalStorage()
</script>
