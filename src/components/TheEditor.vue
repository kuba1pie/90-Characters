<template>
  <div class="c-theEditor">
    <h2>Send a new message</h2>
    <form action="#">
      <div class="form__title">
        <label for="input">Title</label>
        <input
          v-model="newMessage.title"
          placeholder="Enter the title"
          minlength="3"
          maxlength="32"
          name="input"
          :class="{ error: !newMessage.title }"
        >
      </div>
      <div class="form__message">
        <label for="text">Message</label>
        <textarea
          v-model="newMessage.message"
          name="text"
          placeholder="Enter the message here..."
          :class="{ error: !newMessage.message }"
          maxlength="256"
        />
      </div>
      <div class="form__character">
        <label for="select">Character</label>
        <select
          v-model="newMessage.recipient"
          name="select"
          :class="{ error: !newMessage.recipient }"
        >
          <option
            value=""
            disabled
            selected
            hidden
          >
            Pick a character
          </option>
          <option
            v-for="item in store.charactersData.results"
            :key="item.id"
            :value="item.id"
          >
            {{ item.name }}
          </option>
        </select>
      </div>
      <div class="form__checkbox">
        <input
          id="checkbox"
          v-model="newMessage.checkbox"
          type="checkbox"
          name="checkbox"
          class="checkbox"
          required
        >
        <label for="checkbox">I want to use InterGalaxy Quickpost™</label>
      </div>
      <div class="form__button">
        <button
          type="submit"
          :class="{ active: isActive }"
          :disabled="isActive"
          @click="onSubmitClick()"
        >
          Send
        </button>
      </div>
    </form>
  </div>
</template>

<script setup lang="ts">import { Message } from '../types';

const store = useDefaultStore();
store.getCharacters();
let newMessage: Message = reactive({ title: "", message: "", recipient: "", timestamp: new Date(0), checkbox: false });
let archiveData: Message[] = []

const isActive = computed(() => {
  if (newMessage.title === "" || newMessage.message === "" || newMessage.recipient === "" || newMessage.checkbox === false) {
    return true
  }
  else {
    return false
  }
})

async function onSubmitClick() {
  if (window.localStorage.getItem('archiveData')) {
    archiveData = JSON.parse(window.localStorage.getItem('archiveData')!);
    archiveData.push(newMessage)
    window.localStorage.setItem('archiveData', (JSON.stringify(archiveData)));
  }
  else {
    archiveData.push(newMessage)
    window.localStorage.setItem('archiveData', (JSON.stringify(archiveData)));
  }
  newMessage.title = ""
  newMessage.message = ""
  newMessage.recipient = ""
  newMessage.timestamp = new Date(Date.now())
  newMessage.checkbox = false
}
</script>