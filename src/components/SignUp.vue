<template>
  <div class="flex flex-col items-center gap-10">
    <h1 class="text-5xl font-bold tracking-widest text-primary">Sign Up</h1>
    <div class="flex flex-col gap-5 w-96">
      <input
        type="text"
        v-model="name"
        placeholder="Enter name"
        className="input input-bordered w-full  bg-white"
      />
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

      <div class="flex flex-col justify-between gap-5">
        <button v-on:click="signUp" class="w-full btn btn-primary">
          Sign Up
        </button>
        <router-link to="/login" class="w-full btn btn-neutral"
          >Log In</router-link
        >
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "SignUp",
  data() {
    return {
      name: "",
      email: "",
      password: "",
    };
  },
  methods: {
    async signUp() {
      let result = await axios.post("http://localhost:3000/users", {
        name: this.name,
        email: this.email,
        password: this.password,
      });

      if (result.status == 201) {
        localStorage.setItem("user-info", JSON.stringify(result.data));
        this.$router.push({ name: "Home" });
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
