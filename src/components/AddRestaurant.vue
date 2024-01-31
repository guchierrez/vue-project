<template>
  <div class="flex flex-col items-center gap-10">
    <h1 class="text-5xl font-bold tracking-widest uppercase text-primary">
      Add Restaurant
    </h1>
    <div class="flex flex-col gap-5 w-96">
      <input
        type="text"
        v-model="restaurant.name"
        placeholder="Enter restaurant name"
        className="input input-bordered w-full bg-white"
      />

      <input
        type="number"
        v-model="restaurant.contact"
        placeholder="Enter contact number"
        className="input input-bordered w-full bg-white"
      />

      <input
        type="text"
        v-model="restaurant.address"
        placeholder="Enter address"
        className="input input-bordered w-full bg-white"
      />

      <div class="flex flex-col justify-between w-full gap-5">
        <button v-on:click="add" class="w-full btn btn-primary">Create</button>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "Add",

  data() {
    return {
      restaurant: {
        name: "",
        contact: "",
        address: "",
      },
    };
  },

  methods: {
    async add() {
      let result = await axios.post("http://localhost:3000/restaurants", {
        name: this.restaurant.name,
        contact: this.restaurant.contact,
        address: this.restaurant.address,
      });

      if (result.status == 201) {
        this.$router.push({ name: "Home" });
      } else {
        alert("There was a problem creating a restaurant.");
      }
    },
    mounted() {
      let user = localStorage.getItem("user-info");
      if (!user) {
        this.$router.push({ name: "Login" });
      }
    },
  },
};
</script>
