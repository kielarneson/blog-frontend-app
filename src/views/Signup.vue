<template>
  <div class="signup">
    <form v-on:submit.prevent="submit()">
      <h1>Signup</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label>Name:</label>
        <input type="text" v-model="newUserParams.name" />
        <small
          v-if="newUserParams.name.length > 0 && newUserParams.name[0] !== newUserParams.name[0].toUpperCase()"
          class="text-warning"
        >
          Capitalize first name
        </small>
        <small
          v-if="newUserParams.name.length > 0 && newUserParams.name[0] === newUserParams.name[0].toUpperCase()"
          class="text-success"
        >
          Valid first name
        </small>
      </div>
      <div>
        <label>Email:</label>
        <input type="email" v-model="newUserParams.email" />
      </div>
      <div>
        <label>Password:</label>
        <input type="password" v-model="newUserParams.password" />
      </div>
      <div>
        <label>Password confirmation:</label>
        <input type="password" v-model="newUserParams.password_confirmation" />
        <small
          v-if="
            newUserParams.password_confirmation.length >= newUserParams.password.length &&
            newUserParams.password !== newUserParams.password_confirmation
          "
          class="text-warning"
        >
          Does not match
        </small>
        <small
          v-if="newUserParams.password.length > 0 && newUserParams.password === newUserParams.password_confirmation"
          class="text-success"
        >
          Match
        </small>
      </div>
      <input type="submit" value="Submit" />
    </form>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      newUserParams: {
        name: "",
        email: "",
        password: "",
        password_confirmation: "",
      },
      errors: [],
    };
  },
  methods: {
    submit: function () {
      axios
        .post("/users", this.newUserParams)
        .then((response) => {
          console.log(response.data);
          this.$parent.flashMessage = "Successfully signed up";
          this.$router.push("/login");
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>
