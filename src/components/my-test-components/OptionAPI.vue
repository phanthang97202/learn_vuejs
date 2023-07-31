<script>
export default {
  data() {
    return {
      count: 0,
    };
  },
  methods: {
    increament() {
      this.count += 1;
    },
  },
  mounted() {
    this.increament();
  },
};
</script>

<template>
  <button @click="increament">Click (OptionAPI)</button>
  <p>{{ count }}</p>
</template>
