<template>
  <b-sidebar
    id="Avatar"
    title="Choose profile Picture"
    right
    backdrop
    shadow
    width="500px"
  >
    <p class="text-muted small">
      Lorem, ipsum dolor sit amet consectetur adipisicing elit. Dolores eaque
      itaque obcaecati minus ducimus magnam nemo recusandae debitis ?
    </p>
    <div class="d-flex flex-wrap">
      <div v-for="(item, index) in 12" :key="index">
        <b-img
          :src="`/images/profile/avatar-${index + 1}.svg`"
          height="62px"
          :class="
            profile_pic_path == `/images/profile/avatar-${index + 1}.svg`
              ? 'bg-success'
              : 'bg-light'
          "
          class="mb-3 me-3 border rounded cursor-pointer"
          @click="profile_pic_path = `/images/profile/avatar-${index + 1}.svg`"
        />
      </div>
      <b-button variant="dark" @click="UpdateProfile(profile_pic_path)"
        >Save</b-button
      >
    </div>
  </b-sidebar>
</template>

<script>
export default {
  data() {
    return {
      profile_pic_path: "",
    };
  },
  methods: {
    UpdateProfile(path) {
      this.profile_pic_path = path;
      this.$emit("SelctedPhoto", path);
    },
  },
};
</script>

<style></style>
