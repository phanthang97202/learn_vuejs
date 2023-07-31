<template>
  <div class="container mb-3">
    <form action="">
      <div class="container">
        <div class="row">
          <div class="col">
            <div class="mb-3">
              <label for="" class="form-label"> Page Title </label>
              <input type="text" class="form-control" v-model="pageTitle" />
              <!-- :value="pageTitle"
          @input="(e) => (pageTitle = e.target.value)" -->
            </div>
            <div class="mb-3">
              <label for="" class="form-label">Content </label>
              <textarea
                v-model="content"
                type="text"
                class="form-control"
                name=""
                id=""
                cols="30"
                rows="10"
              ></textarea>
            </div>
          </div>
          <div class="col">
            <div class="mb-3">
              <label for="" class="form-label">Link Text</label>
              <input type="text" class="form-control" v-model="linkText" />
            </div>

            <div class="mb-3">
              <label for="" class="form-label">Link Url</label>
              <input type="text" class="form-control" v-model="linkUrl" />
            </div>

            <div class="mb-3">
              <div class="form-check">
                <label for="gridCheck1" class="form-check-label"
                  >Published</label
                >
                <input
                  type="checkbox"
                  class="form-check-input"
                  v-model="published"
                />
              </div>
            </div>
          </div>
        </div>
        <div class="row">
          <div class="mb-3">
            <button
              :disabled="isFormInvalid"
              class="btn btn-primary"
              @click.prevent="submitForm"
            >
              Create Page
            </button>
          </div>
        </div>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  props: ["pageCreated"],
  components: {},
  created() {},

  emits: {
    pageCreated({ pageTitle, content, link }) {
      if (!pageTitle) return false;
      if (!content) return false;
      if (!link || !link.text || !link.url) return false;
      return true;
    },
  },
  // must return value, depend on other data, when data change that excute
  computed: {
    // validation button create page
    isFormInvalid() {
      return (
        !this.pageTitle || !this.content || !this.linkText || !this.linkUrl
      );
    },
  },
  data() {
    return {
      pageTitle: "", // "This is initial value pageTitle",
      content: "", // "This is initial value content",
      linkText: "", //"http://example.com",
      linkUrl: "", //"http://example.com",
      published: true,
    };
  },
  methods: {
    submitForm() {
      if (!this.pageTitle || !this.content || !this.linkText || !this.linkUrl) {
        alert("Please enter value");
        return;
      }

      //   cách 1
      //   this.pageCreated({
      //     pageTitle: this.pageTitle,
      //     content: this.content,
      //     link: {
      //       text: this.linkText,
      //       url: this.linkUrl,
      //     },
      //     published: this.published,
      //   });

      //   cách 2
      this.$emit("pageCreated", {
        pageTitle: this.pageTitle,
        content: this.content,
        link: {
          text: this.linkText,
          url: this.linkUrl,
        },
        published: this.published,
      });

      this.pageTitle = ""; // "This is initial value pageTitle",
      this.content = ""; // "This is initial value content",
      this.linkText = ""; //"http://example.com",
      this.linkUrl = ""; //"http://example.com",
      this.published = true;
    },
  },

  // call every time
  // watcher value props
  watch: {
    pageTitle(newPageTitle, oldPageTitle) {
      console.log(newPageTitle, oldPageTitle);
      if (oldPageTitle === this.linkText) {
        this.linkText = newPageTitle;
      }
    },
  },
};
</script>

<style scoped></style>
