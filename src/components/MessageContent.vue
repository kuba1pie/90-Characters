<template>
  <div
    v-if="recipient"
    class="c-messageContent"
  >
    <div
      class="header"
      @click="showContent = !showContent"
    >
      <div class="title">
        {{ messageData.title }}
      </div>
      <div class="arrowButton">
        <img
          src="../assets/arrow.svg"
          :class="{ rotate: showContent }"
        >
      </div>
    </div>
    <Transition>
      <div
        v-if="showContent"
        class="content"
      >
        <div class="details">
          <img
            :src="recipient.image"
            class="avatar"
          >
          <div class="textInfo">
            <div class="recipient">
              Sent to: {{ recipient.name }}
            </div>
            <div class="date">
              Date: {{ moment(messageData.timestamp).locale("pl").format('L') }}
            </div>
            <div class="time">
              At: {{ moment(messageData.timestamp).locale("pl").format('LT') }}
            </div>
            <div
              v-if="0"
              class="time"
            >
              At: I see what you did there
            </div>
          </div>
        </div>
        <div class="message">
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
