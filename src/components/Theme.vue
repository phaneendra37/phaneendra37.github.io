<template>
  <b-sidebar
    id="theme"
    shadow
    title="Customize theme"
    no-close-on-backdrop
    width="400px"
    lazy
    right
  >
    <div class="border-bottom border-bottom-dashed pb-2 mb-3">
      <div class="mb-2 pb-1">
        <h4 class="mb-1 sidebar-theme-heading">Base Font size</h4>
        <p class="mb-0 small text-muted">
          This will increase or decrease the base font size as per the value
        </p>
      </div>
      <div class="w-100">
        <b-form-input
          v-model="basefontsize"
          type="range"
          min="12"
          max="25"
          @input="ChangeColors('--body-base-font-size', basefontsize + 'px')"
        />
      </div>
    </div>
    <div class="border-bottom border-bottom-dashed pb-2 mb-3">
      <div class="mb-2 pb-1">
        <h4 class="mb-1 sidebar-theme-heading">Base Border radious</h4>
        <p class="mb-0 small text-muted">
          This will increase or decrease the base corner sharpness for gravatar
          etc
        </p>
      </div>
      <div class="w-100">
        <b-form-input
          v-model="baseradious"
          type="range"
          min="0"
          max="100"
          @input="
            ChangeColors('--body-base-border-radious', baseradious + 'px')
          "
        />
      </div>
    </div>
    <div class="border-bottom border-bottom-dashed pb-2 mb-3">
      <div class="mb-2 pb-1">
        <h4 class="mb-1 sidebar-theme-heading">Themes</h4>
        <p class="mb-0 small text-muted">
          This will change the entire window colors , fonts based on themes
        </p>
      </div>
      <div class="d-flex align-items-center flex-wrap">
        <div
          class="color-pellate border cursor-pointer"
          :class="
            selectedtheme == nav.navbar_bg
              ? 'bi bi-check-lg text-success d-flex flex-column align-items-center justify-content-center '
              : ''
          "
          v-for="(nav, index) in themecolors.navbarcolors"
          :key="index"
          :style="`background-color:${nav.navbar_bg};`"
          @click="ChangeColors('--navbar-bg-color', nav.navbar_bg, 'navbarbg')"
        />
      </div>
    </div>
    <div class="border-bottom border-bottom-dashed pb-3 mb-4">
      <div class="mb-2 pb-1">
        <h4 class="mb-1 sidebar-theme-heading">Window background color</h4>
        <p class="mb-0 small text-muted">
          This will change the body color of entire window
        </p>
      </div>
      <div class="d-flex align-items-center flex-wrap">
        <div
          class="color-pellate border cursor-pointer"
          :class="
            selectedbg == bg.body_bg
              ? 'bi bi-check-lg text-success d-flex flex-column align-items-center justify-content-center '
              : ''
          "
          v-for="(bg, index) in themecolors.bodycolors"
          :key="index"
          :style="`background-color:${bg.body_bg};`"
          @click="ChangeColors('--body-bg-color', bg.body_bg, 'selectedbg')"
        />
      </div>
    </div>
    <div class="border-bottom border-bottom-dashed pb-2 mb-3">
      <div class="mb-2 pb-1">
        <h4 class="mb-1 sidebar-theme-heading">Navigation bar color</h4>
        <p class="mb-0 small text-muted">
          This will change the header/navigaton color
        </p>
      </div>
      <div class="d-flex align-items-center flex-wrap">
        <div
          class="color-pellate border cursor-pointer"
          :class="
            navbarbg == nav.navbar_bg
              ? 'bi bi-check-lg text-success d-flex flex-column align-items-center justify-content-center '
              : ''
          "
          v-for="(nav, index) in themecolors.navbarcolors"
          :key="index"
          :style="`background-color:${nav.navbar_bg};`"
          @click="ChangeColors('--navbar-bg-color', nav.navbar_bg, 'navbarbg')"
        />
      </div>
    </div>
  </b-sidebar>
</template>

<script>
import themes from "@/json/theme";
export default {
  name: "Themes",
  data() {
    return {
      basefontsize: 12 + "px",
      baseradious: 2 + "px",
      themecolors: themes,
      selectedbg: "",
      navbarbg: "",
      selectedfont: "",
      selectedtheme: "",
    };
  },
  methods: {
    ChangeColors(colorvar, colorval, active) {
      this.root = document.documentElement;
      this.root.style.setProperty(colorvar, colorval);
      this.activeElement(active, colorval);
    },
    activeElement(el, el_val) {
      this[el] = el_val;
    },
  },
};
</script>

<style></style>
