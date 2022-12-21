<template>
  <b-navbar
    toggleable="md"
    type="dark"
    class="vh-100 py-0 flex-md-column navbar-bg"
  >
    <b-navbar-brand
      to="/"
      class="me-0 text-white d-flex align-items-center nav-link py-4 mb-0 me-auto"
    >
      <b-img src="/images/icon-57.png" height="30" />
      <h3 class="mb-0 h5 ms-2">Apps</h3>
    </b-navbar-brand>
    <b-navbar-toggle target="nav-collapse " class="me-3 p-0 border-0" />
    <b-collapse id="nav-collapse " class="w-100 flex-column" is-nav>
      <b-navbar-nav class="d-flex flex-column mb-auto w-100">
        <li class="nav-item" v-for="(app, index) in apps" :key="index">
          <router-link :to="app.app_url" class="nav-link">
            <i
              :class="`me-2 align-middle bi bi-${
                app.app_icon ? app.app_icon : 'phone'
              }`"
            />
            {{ app.app_name }}
          </router-link>
        </li>
      </b-navbar-nav>
      <b-navbar-nav class="d-flex w-100 border-top mt-3 p-2 border-body">
        <b-dropdown
          variant="link text-white p-0"
          toggle-class=" text-decoration-none"
          no-caret
          menu-class="w-100"
          dropup
        >
          <template #button-content>
            <Gravatar
              name="Phaneendra vfdv"
              :info="true"
              email="kphanedendra337@gmail.com"
              :img_size="35"
            />
          </template>
          <b-dropdown-item v-b-toggle.theme>Themes</b-dropdown-item>
          <b-dropdown-item v-b-toggle.Avatar>Avatar</b-dropdown-item>
          <b-dropdown-item v-b-toggle.profiledetails
            >Profile Details</b-dropdown-item
          >
          <b-dropdown-divider />
          <b-dropdown-item link-class="text-danger">Sign Out</b-dropdown-item>
        </b-dropdown>
      </b-navbar-nav>
    </b-collapse>

    <Theme />
    <Avatar @SelctedPhoto="UpdateProfilePath" />
    <ProfileDetails />
  </b-navbar>
</template>

<script>
import Theme from "./Theme.vue";
import Avatar from "./Avatar.vue";
import ProfileDetails from "./ProfileDetails.vue";
import Apps from "../json/apps/app";
import Gravatar from "./Gravatar.vue";
export default {
  components: { Theme, Avatar, ProfileDetails, Gravatar },
  data() {
    return {
      selectedPhoto: "",
      apps: Apps.apps,
    };
  },
  methods: {
    UpdateProfilePath(data) {
      this.selectedPhoto = data;
    },
  },
};
</script>
