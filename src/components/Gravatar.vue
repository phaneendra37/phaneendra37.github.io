<template>
  <div class="d-flex align-items-center text-start text-truncate">
    <Gravatar :size="img_size" class="rounded" :email="email ? email : name" />
    <div class="ms-2 flex-grow-1 text-truncate" v-if="info">
      <h6 class="mb-1 text-truncate" v-if="name">{{ name }}</h6>
      <p v-if="email" class="small mb-0 text-truncate text-truncate">
        {{ email }}
      </p>
    </div>
  </div>
</template>

<script>
import Gravatar from "vue-gravatar";
export default {
  components: { Gravatar },
  props: {
    name: String,
    email: String,
    img_size: {
      type: Number,
      default: 35,
    },
    info: Boolean,
  },
};
</script>

<style></style>
