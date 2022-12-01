<template>
  <div class="container-fluid px-0">
    <d-flex class="flex-nowrap">
      <Navbar />
      <div class="main-content">
        <router-view />
      </div>
    </d-flex>
  </div>
</template>
<script>
import Navbar from "@/components/Navbar.vue";
export default {
  components: { Navbar },
};
</script>
