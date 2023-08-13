<template>
  <nav
    :class="[
      'navbar',
      'navbar-expand-sm',
      `navbar-${this.theme}`,
      `bg-${this.theme}`,
    ]"
  >
    <div class="container-fluid">
      <a class="navbar-brand" href="#">Navbar</a>
      <ul class="navbar-nav me-auto mt-2 mt-lg-0">
        <navbar-link
          class="nav-item"
          v-for="(page, index) in publishedPages"
          :key="index"
          :page="page"
          :index="index"
        />

        <li>
          <router-link
            to="/pages"
            class="nav-link"
            active-class="active"
            aria-current="page"
            >Pages
          </router-link>
        </li>
      </ul>
      <form class="d-flex">
        <button class="btn btn-outline-success" @click.prevent="changeTheme()">
          Toggle Theme
        </button>
      </form>
    </div>
  </nav>
</template>

<script>
import NavbarLink from './NavbarLink.vue';
export default {
  components: { NavbarLink },
  inject: ['$pages', '$bus'],
  props: ['pages'],
  computed: {
    publishedPages() {
      return this.pages.filter((p) => p.published);
    },
  },
  created() {
    this.getThemeSetting();

    this.pages = this.$pages.getAllPages();

    this.$bus.$on('page-updated', () => {
      this.pages = [...this.$pages.getAllPages()];
    });

    this.$bus.$on('page-created', () => {
      this.pages = [...this.$pages.getAllPages()];
    });

    this.$bus.$on('page-deleted', () => {
      this.pages = [...this.$pages.getAllPages()];
    });
  },
  data() {
    return {
      theme: 'dark',
      pages: [],
    };
  },
  methods: {
    changeTheme() {
      this.theme = this.theme == 'dark' ? 'light' : 'dark';
      this.storeThemeSetting();
    },
    storeThemeSetting() {
      localStorage.setItem('theme', this.theme);
    },
    getThemeSetting() {
      localStorage.getItem('theme');
    },
    getThemeSetting() {
      let theme = localStorage.getItem('theme');

      if (theme) {
        this.theme = theme;
      }
    },
  },
};
</script>

<style></style>
