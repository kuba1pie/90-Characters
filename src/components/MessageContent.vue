<template>
  <div
    v-if="recipient"
    class="c-messageContent border-1 text-6 my-2 p-5"
  >
    <div
      class="head flex"
      @click="showContent = !showContent"
    >
      <div
        class="recipient text-8"
        :class="{ 'text-orange-800/80': messageData.checkbox }"
      >
        {{ recipient.name }}
      </div>
      <div
        class=" arrow text-black arrowButton i-ant-design:arrow-down-outlined"
        :verticalFlip="true"
        :class="{ rotate: showContent }"
      />
      <div class="i-mdi-alarm text-orange-400" />
    </div>
    <Transition>
      <div
        v-if="showContent"
        class="content"
      >
        <div class="details flex my-4">
          <img
            :src="recipient.image"
            class="avatar"
          >
          <div class="textInfo mx-2 text-gray-600">
            <div class="title">
              Subject: {{ messageData.title }}
            </div>
            <div class="date">
              Date: {{ moment(messageData.timestamp).locale("pl").format('L') }}
            </div>
            <div class="time">
              At: {{ moment(messageData.timestamp).locale("pl").format('LT') }}
            </div>
          </div>
        </div>
        <div class="message my-3">
          {{ messageData.message }}
        </div>
      </div>
    </Transition>
  </div>
</template>
<script setup lang="ts">
import { Character, Message } from '../types';
import moment from "moment";

const store = useDefaultStore();
const props = defineProps<{
  messageData: Message
}>()

let recipient: Character
if (store.charactersData) {
  let results: Character = store.charactersData.results
  recipient = results.find((character: { id: string; }) => character.id === props.messageData.recipient)
}
let showContent = ref(false)

</script>
<style lang="scss">
.arrow {
  width: 10px;
  height: 1em;
}

.avatar {
  width: 80px;
  border-radius: 40px;
}
</style>