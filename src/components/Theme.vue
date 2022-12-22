<template>
  <b-sidebar
    id="theme"
    shadow
    title="Customize theme"
    no-close-on-backdrop
    width="450px"
    lazy
    right
  >
    <div class="border-bottom-dashed border-bottom">
      <h4 class="theme-name-heading">Layout Themes</h4>
      <p class="theme-description text-muted">
        This will change the entire window look and feel as per the user
        convinience
      </p>
      <div class="my-3 d-flex flex-wrap">
        <div
          v-for="(theme, index) in themecolors.themes"
          :key="index"
          class="color-pellate cursor-pointer border border-light"
          :style="`background-color:${theme.colors.navbar_bg_color};`"
          @click="ChangeColors('--body-bg-color', theme.colors)"
        />
      </div>
    </div>
    <div class="border-bottom-dashed border-bottom pt-4">
      <h4 class="theme-name-heading">Body Background Color</h4>
      <p class="theme-description text-muted">
        This will change the body backgound color only
      </p>
      <div class="my-3 d-flex flex-wrap">
        <div
          v-for="(theme, index) in themecolors.themes"
          :key="index"
          class="color-pellate cursor-pointer border"
          :style="`background-color:${theme.colors.body_bg_color};`"
          :class="
            selectedbg == theme.colors.body_bg_color
              ? 'border-dark'
              : 'border-light'
          "
          @click="
            ChangeColors(
              'body-bg-color',
              theme.colors.body_bg_color,
              'selectedbg'
            )
          "
        />
      </div>
    </div>
    <div class="border-bottom-dashed border-bottom pt-4">
      <h4 class="theme-name-heading">Menu Background Color</h4>
      <p class="theme-description text-muted">
        This will change the menu background color only
      </p>
      <div class="my-3 d-flex flex-wrap">
        <div
          v-for="(theme, index) in themecolors.themes"
          :key="index"
          :class="
            navbarbg == theme.colors.navbar_bg_color
              ? 'border-dark'
              : 'border-light'
          "
          class="color-pellate cursor-pointer border"
          :style="`background-color:${theme.colors.navbar_bg_color};`"
          @click="
            ChangeColors(
              '--navbar-bg-color',
              {
                'navbar-text-color': theme.colors.navbar_text_color,
                'navbar-bg-color': theme.colors.navbar_bg_color,
              },
              'navbarbg'
            )
          "
        />
      </div>
    </div>
    <div class="border-bottom-dashed border-bottom pt-4">
      <h4 class="theme-name-heading">Font styles</h4>
      <p class="theme-description text-muted">
        This will change displaying of text font changes only
      </p>
      <div class="my-3 d-flex flex-wrap">
        <b-row class="px-2">
          <b-col
            md="6"
            class="px-2 mb-2"
            v-for="(font, index) in fonts"
            :key="index"
            @click="
              ChangeColors(
                'body-font-family',
                font.body_font_family,
                'selectedfont'
              )
            "
          >
            <div
              class="cursor-pointer rounded-1 border text-center p-1 text-truncate"
              :style="`font-family:${font.body_font_family}`"
            >
              {{ font.name }}
            </div>
          </b-col>
        </b-row>
      </div>
    </div>
    <div class="border-bottom-dashed border-bottom py-3 d-flex">
      <h4 class="theme-name-heading text-nowrap me-5 mb-0">Base Font size</h4>
      <b-form-input
        v-model="selectedBaseFontSize"
        type="range"
        min="5"
        class="w-50 ms-auto"
        max="15"
        @input="
          ChangeColors('body-base-font-size', selectedBaseFontSize + 'px')
        "
      />
    </div>
    <div class="border-bottom-dashed border-bottom py-3 d-flex">
      <h4 class="theme-name-heading me-5 mb-0 text-nowrap">Corner sharpness</h4>
      <b-form-input
        v-model="borderradious"
        type="range"
        min="0"
        class="w-50 ms-auto"
        max="50"
        @input="ChangeColors('body-base-border-radious', borderradious + 'px')"
      />
    </div>
    <div class="d-flex justify-content-end py-4">
      <b-button variant="dark" class="px-4" @click="SaveTheme">Save</b-button>
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
      fonts: fonts.fonts,
      themecolors: themes,
      borderradious: 4,
      selectedbg: "",
      navbarbg: "",
      selectedfont: "",
      selectedtheme: "",
      selectedBaseFontSize: 8,
    };
  },
  mounted() {
    var theme = localStorage.getItem("theme");
    if (theme) {
      console.log(theme);
      this.setTheme(theme);
    }
  },
  methods: {
    setTheme(setTheme) {
      this.selectedbg = setTheme.selectedbg;
      this.navbarbg = setTheme.navbarbg;
      this.selectedfont = setTheme.selectedfont;
      this.selectedtheme = setTheme.selectedtheme;
      this.selectedBaseFontSize = setTheme.selectedBaseFontSize;
    },
    ChangeColors(colorvar, colorval, active) {
      if (typeof colorval == "string") {
        return this.AddColor(`--${colorvar}`, colorval, active);
      } else {
        for (var val in colorval) {
          let colorlable = val.replaceAll("_", "-");
          this.AddColor(`--${colorlable}`, colorval[val], active);
        }
      }
    },
    AddColor(colorvar, colorval, active) {
      let colorlable = colorvar.replaceAll("_", "-");
      this.root = document.documentElement;
      this.root.style.setProperty(colorlable, colorval);
      if (active) {
        return this.activeElement(active, colorval);
      }
    },
    activeElement(el, el_val) {
      this[el] = el_val;
    },
    SaveTheme() {
      var config = {
        borderradious: this.borderradious,
        selectedbg: this.selectedbg,
        navbarbg: this.navbarbg,
        selectedfont: this.selectedfont,
        selectedtheme: this.selectedtheme,
        selectedBaseFontSize: this.selectedBaseFontSize,
      };
      localStorage.setItem("theme", JSON.stringify(config));
    },
  },
};
</script>

<style></style>
