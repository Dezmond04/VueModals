<template>
  <modal title="Login" @close="close">
    <div slot="body">
      <form @submit.prevent="onSubmit">
        <div class="form-item" :class="{ errorInput: $v.email.$error }">
          <label>Email</label>
          <p class="errorText" v-if="!$v.email.required">Field is required!</p>
          <p class="errorText" v-if="!$v.email.email">Email is not correct!</p>
          <input
            v-model="email"
            type="email"
            :class="{ error: $v.email.$error }"
            @change="$v.email.$touch()"
          />
        </div>
        <div class="form-item" :class="{ errorInput: $v.password.$error }">
          <label>Password</label>
          <p class="errorText" v-if="!$v.password.required">
            Password is required.
          </p>
          <p class="errorText" v-if="!$v.password.minLength">
            Password must have at least 6 letters.
          </p>
          <input
            v-model="password"
            type="password"
            :class="{ error: $v.password.$error }"
            @change="$v.password.$touch()"
          />
        </div>
        <button class="btn btnPrimary">Registration</button>
      </form>
      <button @click="closeLoginModal()" class="need-registration">
        I need registration
      </button>
    </div>
  </modal>
</template>

<script>
import { required, minLength, email } from "vuelidate/lib/validators";

import modal from "@/components/UI/Modal.vue";

export default {
  components: { modal },
  data() {
    return {
      email: "",
      password: "",
    };
  },
  validations: {
    email: {
      required,
      email,
    },
    password: {
      required,
      minLength: minLength(6),
    },
  },
  methods: {
    onSubmit() {
      this.$v.$touch();
      if (!this.$v.$invalid) {
        const user = {
          email: this.email,
          password: this.password,
        };
        console.log(user);
        // DONE
        this.email = "";
        this.password = "";
        this.$v.$reset();
        this.$emit("close");
      }
    },
    close() {
      this.email = "";
      this.password = "";
      this.$v.$reset();
      this.$emit("close");
    },
    closeLoginModal() {
      this.close();
      this.$emit("openRegistration");
    },
  },
};
</script>

<style scoped>
form {
  margin-bottom: 20px;
}
.need-registration {
  font-size: 14px;
  color: #999999;
  cursor: pointer;
  background-color: transparent;
  border: none;
}
</style>
