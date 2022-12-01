<template>
  <b-container fluid>
    <div id="nav">
      <router-link to="/">Phane</router-link> |
      <router-link to="/about">Priya</router-link>
    </div>
    <router-view />
  </b-container>
</template>
<script>
export default {
  compatConfig: { MODE: 3 },
};
</script>
