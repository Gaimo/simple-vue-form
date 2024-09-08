<template>
  <div class="custom-input">
    <input
      :id="id"
      :type="type"
      :placeholder="placeholder"
      v-model="inputValue"
      @focus="handleFocus"
      @blur="handleBlur"
    />
    <Close
      class="icon"
      :class="{ visible: isFocused && inputValue }"
      @click="clearInput"
    />
  </div>
</template>

<script setup>
import { ref, defineProps } from 'vue';
import Close from '../components/Close.vue';

// Define props to accept the id
const props = defineProps({
  id: {
    type: String,
    required: false,
    default: ""
  },
  type: {
    type: String,
    required: false,
    default: "text"
  },
  placeholder: {
    type: String,
    required: false,
    default: ""
  }

});

const sleep = (ms) => new Promise((resolve) => setTimeout(resolve, ms));

const handleFocus = () => {
  isFocused.value = true;
};

const handleBlur = async () => {
  await sleep(100);
  isFocused.value = false;
};

const isFocused = ref(false);
const inputValue = ref('');

const clearInput = () => {
  inputValue.value = '';
};
</script>

<style scoped>
.visible {
  opacity: 100% !important;
}

.icon {
  width: 16px;
  height: 16px;
  color: white;
  cursor: pointer;
  margin-right: 8px;
  opacity: 0%;
}

.custom-input {
  display: flex;
  align-items: center;
  border: 1px solid white;
  min-width: 200px;
  border-radius: 4px;
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
