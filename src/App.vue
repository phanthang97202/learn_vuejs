<template>
  <navbar
    :pages="pages"
    :active-page="activePage"
    :nav-link-click="(index) => (activePage = index)"
  >
  </navbar>
  <!-- <div v-show="true">Hidden content</div> -->
  <!-- nếu không có v-if thì nó sẽ xuất hiện 2 thanh navbar  -->
  <page-viewer :page="pages[activePage]"> </page-viewer>
  <!-- <page-viewer v-if="pages.length > 0" :page="pages[activePage]"> </page-viewer> -->

  <!-- cách 1  -->
  <!-- <create-page :page-created="pageCreated"> </create-page> -->

  <!-- emit event  -->
  <create-page @page-created="pageCreated"> </create-page>
</template>

<script>
import Navbar from "./components/Navbar.vue";
import PageViewer from "./components/PageViewer.vue";
import CreatePage from "./components/CreatePage.vue";
import { reactive } from "vue";
export default {
  components: {
    Navbar,
    PageViewer,
    CreatePage,
  },
  created() {
    this.getPages();
  },
  data() {
    return {
      activePage: 0,
      pages: [],
      // pages: this.getPages(),
    };
  },
  methods: {
    async getPages() {
      let res = await fetch("pages.json");
      let data = await res.json();
      this.pages = data;
      // return data;
    },

    pageCreated(pageObj) {
      console.log("===pageObj", pageObj, [...this.pages, reactive(pageObj)]);
      // this.pages = [...this.pages, reactive(pageObj)];
      this.pages.push(reactive(pageObj));
    },
  },
};
</script>

<style scoped></style>
