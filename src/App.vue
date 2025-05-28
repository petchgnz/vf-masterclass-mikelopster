<script setup>
import { ref, computed, onMounted, watch } from 'vue';

const isValid = ref(true);
const isUpdated = ref(false);
const isLoading = ref(false);
const firstName = ref('');
const lastName = ref('');
const email = ref('');
const errors = ref({});

const fullName = computed(() => {
  return `${firstName.value} ${lastName.value}`;
});

onMounted(() => {
  firstName.value = 'test';
  lastName.value = 'test 2';
  email.value = 'test@mail.com';
});

const updateProfile = async () => {
  isLoading.value = true;
  await new Promise((resolve) => setTimeout(resolve, 2000));
  isLoading.value = false;
  isUpdated.value = true;
};

const validateName = (name) => {
  const re = /\d/;
  return !re.test(name);
};

const validateEmail = (email) => {
  return email.includes('@');
};

watch([firstName, lastName, email], () => {
  isValid.value = true;
  isUpdated.value = false;
  errors.value = {};

  if (!validateName(firstName.value)) {
    errors.value.firstName = 'Invalid First name!';
    isValid.value = false;
  }
  if (!validateName(lastName.value)) {
    errors.value.lastName = 'Invalid Last name!';
    isValid.value = false;
  }
  if (!validateEmail(email.value)) {
    errors.value.email = 'Invalid Email!';
    isValid.value = false;
  }
});
</script>

<template>
  <div class="container">
    <!-- Display Name and Email -->
    <div>
      <div>Fullname: {{ fullName }}</div>
      <div>Email: {{ email }}</div>
    </div>

    <!-- First name Input -->
    <div>
      <div>Firstname:</div>
      <input
        type="text"
        v-model="firstName"
      />
      <div class="error">{{ errors.firstName }}</div>
    </div>

    <!-- Last name Input -->
    <div>
      <div>Lastname:</div>
      <input
        type="text"
        v-model="lastName"
      />
      <div class="error">{{ errors.lastName }}</div>
    </div>

    <!-- Email Input -->
    <div>
      <div>Email:</div>
      <input
        type="text"
        v-model="email"
      />
      <div class="error">{{ errors.email }}</div>
    </div>

    <!-- is Loading UI -->
    <div
      class="loading"
      v-if="isLoading"
    >
      Loading...
    </div>

    <!-- Profile Updated -->
    <div
      class="loading"
      v-if="isUpdated"
    >
      Profile Updated
    </div>

    <!-- Update Button -->
    <button
      :disabled="!isValid"
      class="button"
      @click="updateProfile"
    >
      Update Profile
    </button>
  </div>
</template>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.container {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  max-width: 320px;
  margin: 0 auto;
  height: 100vh;

  div {
    width: 100%;
  }

  .button {
    width: 100%;
    height: 30px;
    margin-top: 20px;
  }

  .loading {
    background: aliceblue;
    width: 100%;
    padding: 20px;
    margin: 10px 0;
    text-align: center;
  }

  .error {
    color: red;
  }
}

input {
  width: 100%;
}
</style>
