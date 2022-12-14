<template>
  <div id="app">
    <div id="nav">
      <div class="d-md-flex flex-md-nowrap">
        <Navbar class="vh-100 overflow-auto" />
        <div class="flex-grow-1">
          <b-container fluid>
            <b-container class="pt-3">
              <router-view />
            </b-container>
          </b-container>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import Navbar from "./components/Navbar.vue";
export default {
  name: "AppHeart",
  components: { Navbar },
};
</script>
