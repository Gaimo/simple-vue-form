<template>
  <div class="custom-input">
    <input
      type="password"
      placeholder="enter your password"
      v-model="password"
      @focus="handleFocus"
      @blur="handleBlur"
    />
    <Close
      class="icon"
      :class="{ hide: !isFocused && !password }"
      @click="clearInput"
    />
  </div>
</template>

<script setup>
import { ref } from 'vue';
import Close from '../components/Close.vue';

const sleep = (ms) => new Promise((resolve) => setTimeout(resolve, ms));

const handleFocus = () => {
  isFocused.value = true;
};

const handleBlur = async () => {
  await sleep(100);
  isFocused.value = false;
};

const isFocused = ref(false);
const password = ref('');

const clearInput = () => {
  password.value = '';
};
</script>

<style scoped>
.hide {
  opacity: 0%;
}

.icon {
  width: 16px;
  height: 16px;
  color: white;
  cursor: pointer;
  margin-right: 8px;
}

.custom-input {
  display: flex;
  align-items: center;
  border: 1px solid white;
  min-width: 200px;
}

.custom-input input {
  border: none;
  background-color: transparent;
  padding: 8px;
  flex-grow: 1;
}

.custom-input input:focus {
  border: none;
  outline: none;
}
</style>
