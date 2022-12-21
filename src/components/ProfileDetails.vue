<template>
  <b-sidebar
    lazy
    id="profiledetails"
    width="400px"
    right
    title="Profile Details"
    shadow
    no-close-on-backdrop
    backdrop
  >
    <p class="mb-0 text-muted small">
      Lorem ipsum dolor sit amet consectetur adipisicing elit. Natus, iste?
      Inventore tempore dolorum similique veritatis repellendus.
    </p>
    <b-form @submit="SaveProfileDetails()">
      <b-row class="mt-3">
        <b-col md="12">
          <b-form-group label="Name" label-class="pb-0">
            <b-form-input
              type="text"
              placeholder="Enter you name"
              required
              v-model="form.name"
            />
          </b-form-group>
        </b-col>
        <b-col md="12">
          <b-form-group label="Email" label-class="pb-0">
            <b-form-input
              type="email"
              placeholder="Enter your email"
              readonly
              required
              v-model="form.email"
            />
          </b-form-group>
        </b-col>
        <b-col md="12">
          <b-form-group label="Phone Number" label-class="pb-0">
            <b-form-input
              type="number"
              placeholder="Enter your phone number"
              required
              v-model="form.mobile_number"
            />
          </b-form-group>
        </b-col>
        <b-col md="12">
          <b-button type="submit" variant="dark">Submit</b-button>
        </b-col>
      </b-row>
    </b-form>
  </b-sidebar>
</template>

<script>
export default {
  data() {
    return {
      form: {
        name: "",
        email: "",
        mobile_number: "",
      },
    };
  },
};
</script>
<style></style>
