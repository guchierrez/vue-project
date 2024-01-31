<template>
  <div class="flex flex-col items-center gap-10">
    <h1 class="text-5xl font-bold tracking-widest uppercase text-primary">
      Update Restaurant
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
        <button v-on:click="update" class="w-full btn btn-primary">
          Update
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "Update",

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
    async update() {
      let result = await axios.put(
        "http://localhost:3000/restaurants/" + this.$route.params.id,
        {
          name: this.restaurant.name,
          contact: this.restaurant.contact,
          address: this.restaurant.address,
        }
      );

      if (result.status == 200) {
        this.$router.push({ name: "Home" });
      } else {
        alert("There was a problem updating the restaurant.");
      }
    },
    mounted() {
      let user = localStorage.getItem("user-info");
      if (!user) {
        this.$router.push({ name: "Login" });
      }
    },
  },

  async mounted() {
    let user = localStorage.getItem("user-info");
    if (!user) {
      this.$router.push({ name: "Login" });
    }

    let result = await axios.get(
      "http://localhost:3000/restaurants/" + this.$route.params.id
    );
    this.restaurant = result.data;
  },
};
</script>
