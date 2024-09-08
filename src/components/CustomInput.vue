<template>
  <div class="custom-input">
    <input
      :id="id"
      :type="type"
      :placeholder="placeholder"
      v-model="internalValue"
      @focus="handleFocus"
      @blur="handleBlur"
    />
    <Close
      class="icon"
      :class="{ visible: isFocused && internalValue }"
      @click="clearInput"
    />
  </div>
</template>

<script setup>
import { ref, defineProps, watch } from 'vue';
import Close from '../components/Close.vue';

// Define props to accept the id, type, and placeholder, as well as the modelValue
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
  },
  modelValue: {
    type: String,
    required: false,
    default: ''
  }
});

// Emit the value when it changes
const emit = defineEmits(['update:modelValue']);

// Internal value to bind with the input field
const internalValue = ref(props.modelValue);

// Watch for changes in modelValue prop to keep internalValue in sync
watch(() => props.modelValue, (newValue) => {
  internalValue.value = newValue;
});

// Watch for changes in internalValue and emit them
watch(internalValue, (newValue) => {
  emit('update:modelValue', newValue);
});

const isFocused = ref(false);

const handleFocus = () => {
  isFocused.value = true;
};

const handleBlur = async () => {
  await sleep(100);
  isFocused.value = false;
};

const sleep = (ms) => new Promise((resolve) => setTimeout(resolve, ms));

const clearInput = () => {
  internalValue.value = ''; // Clears the input
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
