<template>
  <div v-if="recipient" class="c-messageContent border-1 text-6 my-2 p-5">
    <div class="head flex justify-between" @click="showContent = !showContent">
      <div class="recipient text-8" :class="{ 'text-orange-800/80': messageData.checkbox }">
        {{  recipient.name  }}
      </div>
      <div class="icon">
        <i class="arrow" :class="{ up: showContent, down: !showContent }"></i>
      </div>
    </div>
    <Transition>
      <div v-if="showContent" class="content">
        <div class="details flex my-4">
          <img :src="recipient.image" class="avatar">
          <div class="textInfo mx-2 text-gray-600">
            <div class="title">
              Subject: {{  messageData.title  }}
            </div>
            <div class="date">
              Date: {{  moment(messageData.timestamp).locale("pl").format('L')  }}
            </div>
            <div class="time">
              At: {{  moment(messageData.timestamp).locale("pl").format('LT')  }}
            </div>
          </div>
        </div>
        <div class="message my-3">
          {{  messageData.message  }}
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
.avatar {
  width: 80px;
  height: 80px;
  border-radius: 40px;
}

.arrow {
  border: solid black;
  border-width: 0 3px 3px 0;
  display: inline-block;
  padding: 3px;
  height: 0.7em;
  width: 0.7em;
  margin-right: 0;
}

.up {
  transform: rotate(-135deg);
  -webkit-transform: rotate(-135deg);
  transition: 0.5s;
}

.down {
  transform: rotate(45deg);
  -webkit-transform: rotate(45deg);
  transition: 0.5s;
}

.v-enter-active,
.v-leave-active {
  transition: opacity 0.5s ease;
}

.v-enter-from,
.v-leave-to {
  opacity: 0;
}
</style>