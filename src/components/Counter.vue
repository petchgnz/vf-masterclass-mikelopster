<script setup>
import { ref, defineProps, onMounted } from 'vue';

const count = ref(0);

onMounted(() => {
    console.log(`On mounted at Counter.Vue`)
})

defineProps({
  messageText: String,
  changeMessage: Function,
});

const increaseCounter = () => {
  count.value += 1;
};
</script>

<template>
  <div>Hello {{ messageText }}</div>

  <div>
    <input
      type="text"
      v-model="watMessage"
    />
    <button @click="changeMessage(watMessage)">Change message from Counter</button>
  </div>

  <button @click="increaseCounter">Click {{ count }}</button>
</template>

<style></style>
