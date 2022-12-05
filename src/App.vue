<template>
  <div class="container-fluid px-0">
    <div class="flex-nowrap d-lg-flex">
      <Navbar class="main-nav" />
      <div class="main-content flex-grow-1">
        <router-view />
      </div>
    </div>
  </div>
</template>
<script>
import Navbar from "@/components/Navbar.vue";
export default {
  components: { Navbar },
};
</script>
