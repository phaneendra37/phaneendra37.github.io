<template>
  <b-sidebar
    id="theme"
    shadow
    title="Customize theme"
    backdrop
    no-close-on-backdrop
    width="400px"
    lazy
    right
  >
    <div>
      <h4 class="mb-2 sidebar-theme-heading">Body Background color</h4>
      <p class="mb-0"></p>
    </div>
  </b-sidebar>
</template>

<script>
export default {
  name: "Themes",
  mounted() {
    this.$root.$emit("bv::toggle::collapse", "theme");
  },
};
</script>

<style></style>
