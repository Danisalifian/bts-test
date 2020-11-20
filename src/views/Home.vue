<template>
  <div class="home">
    <div class="container ">
      <b-tabs v-model="activeTab" type="is-boxed">
        <b-tab-item label="Register">
          <register />
        </b-tab-item>

        <b-tab-item label="Login">
          <login />
        </b-tab-item>
      </b-tabs>
    </div>
  </div>
</template>

<script>
import Register from "../components/Register.vue";
import Login from "../components/Login.vue";

export default {
  name: "Home",
  components: {
    Register,
    Login,
  },
  data() {
    return {
      activeTab: 0,
    };
  },
};
</script>
