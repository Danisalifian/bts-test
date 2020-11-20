<template>
  <section>
    <b-field label="Username">
      <b-input v-model="user.username"></b-input>
    </b-field>
    <b-field label="Email">
      <b-input type="email" v-model="user.email"></b-input>
    </b-field>
    <b-field label="Password">
      <b-input type="password" v-model="user.password" password-reveal>
      </b-input>
    </b-field>
    <b-button type="is-primary" @click="register">Register</b-button>
  </section>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      user: {
        username: "",
        email: "",
        password: "",
      },
    };
  },
  methods: {
    register() {
      axios.post("http://18.139.50.74:8080/register", this.user).then((res) => {
        this.$buefy.toast.open({
          message: res.data.message,
          type: "is-success",
        });
      });
    },
  },
};
</script>
