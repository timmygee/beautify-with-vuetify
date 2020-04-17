<template>
<v-container>
  <v-row>
    <v-col>
      <h1>Signup</h1>
      <v-form ref="signupForm" v-model="formValidity">
        <v-text-field
          label="Email"
          type="email"
          v-model="email"
          :rules="emailRules"
          required
        />
        <v-autocomplete
          label="Which browser do you use?"
          :items="browsers"
        />
        <v-file-input
          label="Attach profile picture"
        />
        <v-text-field
          label="Birthday"
          v-model="birthday"
          readonly
        />
        <v-date-picker
         v-model="birthday"
        />
        <v-checkbox
          label="Agree to terms"
          :rules="agreeToTermsRules"
          required
        />
        <v-btn
          class="mr-4"
          type="submit"
          color="primary"
          :disabled="!formValidity"
        >
          Submit
        </v-btn>
        <v-btn
          class="mr-4"
          color="warning"
          @click="resetValidation"
        >
          Reset Validation
        </v-btn>
        <v-btn
          class="mr-4"
          color="success"
          @click="validateForm"
        >
          Validate Form
        </v-btn>
        <v-btn
          class="mr-4"
          color="error"
          @click="resetForm"
        >
          Reset
        </v-btn>
      </v-form>
    </v-col>
  </v-row>
</v-container>
</template>

<script>
export default {
  data: () => ({
    agreeToTerms: false,
    agreeToTermsRules: [value => !!value || "You must agree to the terms"],
    birthday: "",
    browsers: ["Chrome", "Safari", "Firefox", "Edge", "Brave"],
    email: "",
    emailRules: [
      value => !!value || "Email is required",
      value =>
        (value && value.indexOf("@") !== 0) ||
        "Email should include a username",
      value => (value && value.includes("@")) || "Email needs an @ symbol",
      value =>
        (value && value.indexOf(".") - value.indexOf("@") > 1) ||
        "Email should contain a valid domain",
      value =>
        (value && value.indexOf(".") <= value.length - 3) ||
        "Email should contain a valid domain"
    ],
    formValidity: false
  }),
  methods: {
    resetForm() {
      this.$refs.signupForm.reset();
    },
    resetValidation() {
      this.$refs.signupForm.resetValidation();
    },
    validateForm() {
      this.$refs.signupForm.validate();
    }
  }
};
</script>

<style>
</style>