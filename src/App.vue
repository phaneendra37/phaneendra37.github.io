<template>
  <nav>
    <router-link to="/" class="bg-green-600">Home</router-link> |
    <router-link to="/about">About</router-link>
  </nav>
  <button class="btn-primary" @click="isSideBar = true">Sidebar</button>
  <globalCanvas
    v-bind="{ ...sidebar?.sidebar, isOpen: isSideBar }"
    @cancel="closeSidebar"
    @close="closeSidebar"
    @save="closeSidebar"
  />
  <router-view />
</template>
<script setup>
import { ref } from "vue";
import globalCanvas from "@/components/globalCanvas.vue";
import sidebar from "@/json/sidebar.json";

const isSideBar = ref(true);

const closeSidebar = () => {
  isSideBar.value = false;
};
</script>
