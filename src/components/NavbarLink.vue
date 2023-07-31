<template>
  <a
    class="nav-link"
    :class="activeClasses"
    aria-current="page"
    v-bind:href="page.link.url"
    :title="`This link goes to ${page.link.text}`"
  >
    {{ page.link.text }}
  </a>
</template>

<script>
export default {
  props: ["page", "isActive"],
  computed: {
    activeClasses() {
      return {
        active: this.isActive,
        emphasize: this.isActive,
        colorChange: this.isActive,
      };
    },
  },
};
</script>

<style>
.emphasize {
  text-decoration: underline !important;
}
.colorChange {
  color: blue !important;
}
</style>
