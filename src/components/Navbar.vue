<template>
  <nav
    class="navbar navbar-expand-lg navbar-custom navbar-dark bg-custom vh-100 overflow-y-auto overflow-x-hidden flex-lg-column d-lg-flex py-lg-4 p-3"
  >
    <a class="navbar-brand me-0 py-0 d-flex align-items-center" to="/">
      <img src="/images/icon-57.png" height="30" width="30" />
      <div class="ps-2">
        <h6 class="mb-0">Feature Apps</h6>
      </div>
    </a>
    <button
      class="navbar-toggler p-0 border-0"
      type="button"
      data-bs-toggle="collapse"
      data-bs-target="#navbarNavAltMarkup"
      aria-controls="navbarNavAltMarkup"
      aria-expanded="false"
      aria-label="Toggle navigation"
    >
      <span class="navbar-toggler-icon"></span>
    </button>
    <div
      class="collapse navbar-collapse h-100 w-100 align-items-baseline mt-3"
      id="navbarNavAltMarkup"
    >
      <div class="navbar-nav d-flex flex-column w-100">
        <a class="nav-link active" aria-current="page" href="#">Home</a>
        <a class="nav-link" href="#">Features</a>
        <a class="nav-link" href="#">Pricing</a>
        <a class="nav-link disabled" href="#" tabindex="-1" aria-disabled="true"
          >Disabled</a
        >
      </div>
    </div>
  </nav>
</template>

<script>
export default {};
</script>

<style></style>
