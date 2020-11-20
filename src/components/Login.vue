<template>
  <section>
    <b-field label="Username">
      <b-input v-model="user.username"></b-input>
    </b-field>
    <b-field label="Password">
      <b-input type="password" v-model="user.password" password-reveal>
      </b-input>
    </b-field>
    <b-button type="is-primary" @click="login">Login</b-button>
  </section>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      user: {
        username: "",
        password: "",
      },
    };
  },
  methods: {
    login() {
      axios.post("http://18.139.50.74:8080/login", this.user).then((res) => {
        this.$cookies.set("user_session", res.data.data.token);
        this.$router.push({ name: "Checklist" });
        this.$buefy.toast.open({
          message: "Logged In",
          type: "is-success",
        });
      });
    },
  },
};
</script>
