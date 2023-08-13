<template>
  <div v-if="page" class="container">
    <h1>{{ page.pageTitle }}</h1>
    <p>{{ page.content }}</p>
  </div>
</template>

<script>
export default {
  props: ['index'],
  inject: ['$pages'],
  created() {
    this.page = this.$pages.getSinglePage(this.index);

    this.$watch(
      () => this.$route.params,
      (newParams, prevParams) => {
        console.log('new params:', newParams);
        this.page = this.$pages.getSinglePage(newParams.index);
        console.log('new page:', this.page);
      }
    );
  },
  data() {
    return {
      page: null,
    };
  },
  watch: {
    index(newIndex, prevIndex) {
      console.log('new params:', newIndex);
      this.page = this.$pages.getSinglePage(newIndex);
      console.log('new page:', this.page);
    },
  },
};
</script>

<style></style>
