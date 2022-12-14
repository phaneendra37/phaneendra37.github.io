<template>
  <b-navbar
    class="navbar-bg d-flex flex-md-column py-3"
    toggleable="md"
    type="dark"
  >
    <b-navbar-brand
      to="/"
      class="mb-md-3 mre-0 py-0 text-white d-flex align-items-center px-3"
    >
      <b-img src="/images/icon-57.png" height="30" />
      <h3 class="mb-0 h5 ms-2">Apps</h3>
    </b-navbar-brand>
    <b-navbar-toggle
      target="nav-collapse"
      class="me-3 p-0 border-0"
    ></b-navbar-toggle>
    <b-collapse id="nav-collapse" class="w-100" is-nav>
      <b-navbar-nav class="d-flex flex-column mb-auto w-100">
        <!--<router-link to="/" class="nav-link">Home</router-link>-->
        <b-nav-item v-b-toggle.theme>Themes</b-nav-item>
      </b-navbar-nav>
    </b-collapse>
    <Theme />
    <ManageUsers />
  </b-navbar>
</template>

<script>
import Theme from "./Theme.vue";
export default {
  components: { Theme },
};
</script>
