<template>
  <div class="container">
    <h1>{{ page.pageTitle }}</h1>
    <h1>{{ page.content }}</h1>
  </div>
</template>

<script>
export default {
  // props: ["page"],
  props: {
    page: {
      type: Object,
      default(rawProps) {
        return {
          pageTitle: "",
          content: "",
        };
      },
    },
  },
};
</script>
