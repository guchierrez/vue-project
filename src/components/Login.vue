<template>
  <div class="flex flex-col items-center gap-10">
    <h1 class="text-5xl font-bold tracking-widest text-primary">Login</h1>
    <div class="flex flex-col gap-5 w-96">
      <input
        type="text"
        v-model="email"
        placeholder="Enter email"
        className="input input-bordered w-full bg-white"
      />

      <input
        type="password"
        v-model="password"
        placeholder="Enter password"
        className="input input-bordered w-full bg-white"
      />

      <div class="flex flex-col justify-between w-full gap-5">
        <button v-on:click="login" class="w-full btn btn-primary">Login</button>
        <router-link to="/signup" class="w-full btn btn-neutral"
          >Sign Up</router-link
        >
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "Login",

  data() {
    return {
      email: "",
      password: "",
    };
  },

  methods: {
    async login() {
      let result = await axios.get(
        `http://localhost:3000/users?email=${this.email}&password=${this.password}`
      );

      if (result.status == 200 && result.data.length > 0) {
        localStorage.setItem("user-info", JSON.stringify(result.data[0]));
        this.$router.push({ name: "Home" });
      } else {
        alert("Wrong email/password.");
      }
    },
    mounted() {
      let user = localStorage.getItem("user-info");
      if (user) {
        this.$router.push({ name: "Home" });
      }
    },
  },
};
</script>
