<template>
  <div class="c-theArchive flex flex-col w-200">
    <h2>Message history</h2>
    <div v-if="store.archiveMessages">
      <MessageContent
        v-for="item in store.archiveMessages"
        :key="item"
        :message-data="item"
      />
    </div>
    <div
      v-else
      class="error text-red-800/90 flex flex-col"
    >
      No send messages yet
      <button
        type="submit"
        class="c-tabButton bg-grey-500/20 px-8 py-3 text-8 w-80 m-0 my-10 border-0"
        @click="store.activeTab = 'TheEditor'"
      >
        Go to Editor
      </button>
    </div>
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
