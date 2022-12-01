<template>
  <b-container fluid>
    <div id="nav">
      <router-link to="/"
        ><i class="bi-github" role="img" aria-label="GitHub"></i>
        Phane</router-link
      >
      |
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
