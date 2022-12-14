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
    <div class="border-bottom border-bottom-dashed pb-3 mb-4">
      <h4 class="mb-1 sidebar-theme-heading">Themes</h4>
      <p class="mb-0 small text-muted">
        Help to give a website a unique and stylish look that stands out among
        the crowd.
      </p>
      <div class="d-flex align-items-center flex-wrap mt-3">
        <div
          class="color-pellate border cursor-pointer"
          v-for="(theme, index) in themecolors.themes"
          :key="index"
          :style="`background-color:${theme.colors.navbar_bg_color};`"
          @click="ChangeColors('--body-bg-color', theme.colors)"
        />
      </div>
    </div>
    <div class="border-bottom border-bottom-dashed pb-3 mb-4">
      <h4 class="mb-1 sidebar-theme-heading">Font Styles</h4>
      <p class="mb-0 small text-muted">
        It allows you to specify a variety of fonts
      </p>
      <div class="mt-2">
        <div
          class="mb-1 cursor-pointer"
          v-for="(font, index) in fonts"
          :key="index"
          @click="
            AppendFontURL(font.url);
            ChangeColors('boy_font_family', font.boy_font_family);
          "
        >
          {{ font.name }}
        </div>
      </div>
    </div>
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
          @input="ChangeColors('body_base_font_size', basefontsize + 'px')"
        />
      </div>
    </div>

    <div class="border-bottom border-bottom-dashed pb-2 mb-3">
      <h4 class="mb-1 sidebar-theme-heading">Menu Color</h4>
      <div class="d-flex align-items-center flex-wrap mt-3">
        <div
          class="color-pellate border cursor-pointer"
          v-for="(theme, index) in themecolors.themes"
          :key="index"
          :style="`background-color:${theme.colors.navbar_bg_color};`"
          @click="ChangeColors('navbar_bg_color', theme.colors.navbar_bg_color)"
        />
      </div>
    </div>
    <div class="border-bottom border-bottom-dashed pb-2 mb-3">
      <h4 class="mb-1 sidebar-theme-heading">Body Color</h4>
      <div class="d-flex align-items-center flex-wrap mt-3">
        <div
          class="color-pellate border cursor-pointer"
          v-for="(theme, index) in themecolors.themes"
          :key="index"
          :style="`background-color:${theme.colors.body_bg_color};`"
          @click="ChangeColors('body_bg_color', theme.colors.body_bg_color)"
        />
      </div>
    </div>
    <div class="border-bottom border-bottom-dashed pb-2 mb-3">
      <h4 class="mb-1 sidebar-theme-heading">Border radious</h4>
    </div>
    <div class="border-bottom border-bottom-dashed pb-2 mb-3">
      <h4 class="mb-1 sidebar-theme-heading">Menu Placement</h4>
    </div>
  </b-sidebar>
</template>

<script>
import themes from "@/json/themes/themes.js";
import fonts from "@/json/themes/fonts.js";
export default {
  name: "Themes",
  data() {
    return {
      colorthemes: themes.themes,
      fonts: fonts.fonts,
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
      if (typeof colorval == "string") {
        return this.AddColor(`--${colorvar}`, colorval, active);
      } else {
        for (var val in colorval) {
          let colorlable = val.replaceAll("_", "-");
          this.AddColor(`--${colorlable}`, colorval[val]);
        }
      }
    },
    AddColor(colorvar, colorval, active) {
      let colorlable = colorvar.replaceAll("_", "-");
      this.root = document.documentElement;
      this.root.style.setProperty(colorlable, colorval);
      if (active) return this.activeElement(active, colorval);
    },
    activeElement(el, el_val) {
      this[el] = el_val;
    },
    AppendFontURL(url) {
      var fontUrl = document.getElementById("fontThemes");
      fontUrl.href = url;
    },
  },
};
</script>

<style></style>
