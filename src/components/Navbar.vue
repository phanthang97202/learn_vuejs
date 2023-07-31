<template>
  <nav
    :class="[`navbar-${theme}`, `bg-${theme}`, 'navbar', 'navbar-expand-lg']"
  >
    <div class="container-fluid">
      <a class="navbar-brand" href="#">My Vue</a>
      <ul class="navbar-nav me-auto mb-2 mb-lg-0">
        <li
          class="nav-item"
          v-for="(page, index) in publishedPages"
          :key="index"
        >
          <navbar-link
            :page="page"
            :isActive="activePage === index"
            @click.prevent="navLinkClick(index)"
          >
          </navbar-link>

          <!-- <a
            class="nav-link"
            :class="{ active: activePage == index }"
            aria-current="page"
            v-bind:href="page.link.url"
            :title="`This link goes to ${page.link.text}`"
            @click.prevent="navLinkClick(index)"
          >
            {{ page.link.text }}
          </a> -->
        </li>
      </ul>

      <form class="d-flex">
        <button class="btn btn-primary" @click.prevent="changeTheme()">
          Toggle
        </button>
      </form>
    </div>
  </nav>
</template>

<script>
import NavbarLink from "./NavbarLink.vue";
export default {
  components: {
    NavbarLink,
  },
  props: ["pages", "activePage", "navLinkClick"],
  data() {
    return {
      theme: "light",
    };
  },
  created() {
    this.getThemeSetting();
  },
  computed: {
    publishedPages() {
      return this.pages.filter((p) => p.published);
    },
  },
  methods: {
    changeTheme() {
      let theme = "light";
      if (this.theme === "light") {
        console.log("this", this, this.theme);
        theme = "dark";
      }
      this.theme = theme;
      this.storeThemeSetting();
    },
    storeThemeSetting() {
      localStorage.setItem("theme", this.theme);
    },
    getThemeSetting() {
      let theme = localStorage.getItem("theme");
      theme ? (this.theme = theme) : changeTheme();
    },
  },
};
</script>

<style></style>
