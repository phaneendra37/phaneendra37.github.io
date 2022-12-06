<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </div>
    <i class="bi bi-x" />
    <Themes />
    <router-view />
  </div>
</template>
<script>
import Themes from "@/components/Theme.vue";
export default {
  name: "AppHeart",
  components: { Themes },
};
</script>
