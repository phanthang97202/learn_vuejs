<template>
  <div>
    <!-- Using v-model to achieve two-way binding -->
    <input type="text" v-model="localMessage" />
  </div>
</template>

<script>
import { defineProps, defineEmits, ref, watch } from "vue";

export default {
  props: {
    modelValue: {
      type: String,
      required: true,
    },
  },
  setup(props, { emit }) {
    // Define a reactive variable to store the local value
    const localMessage = ref(props.modelValue);

    // Watch for changes to the local value and emit the event
    watch(localMessage, (newValue) => {
      emit("update:modelValue", newValue);
    });

    return {
      localMessage,
    };
  },
};
</script>
