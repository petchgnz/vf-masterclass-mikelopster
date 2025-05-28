<script setup>
import { ref, reactive, watchEffect, watch } from 'vue';
const fullname = ref('');

const formData = reactive({
  firstname: '',
  lastname: '',
});

watchEffect(() => {
  console.log(`WatchEffect: ${formData}`);
  fullname.value = `${formData.firstname} ${formData.lastname}`;
});

watch(formData, (newFormData, oldFormData) => {
    console.log(`Watch: ${formData}`)
}, { immediate: true})

</script>

<template>
  <div>
    <div>Fullname : {{ fullname }}</div>
    <input
      type="text"
      v-model="formData.firstname"
    />
    <input
      type="text"
      v-model="formData.lastname"
    />
  </div>
</template>
