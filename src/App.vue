<template>
  <navbar />
  <router-view></router-view>
  <!-- <page-viewer :page="pages[activePage]" v-if="pages.length > 0" />
  <create-page @page-created="pageCreated"></create-page> -->
</template>

<script>
import Navbar from './components/Navbar.vue';

export default {
  components: {
    Navbar,
  },
  methods: {
    pageCreated(pageObj) {
      this.pages.push(pageObj);
      console.log(pageObj);
    },
  },
};
</script>
