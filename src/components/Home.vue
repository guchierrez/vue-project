<template>
  <div class="flex flex-col items-center gap-10">
    <h1 class="text-5xl font-bold tracking-widest uppercase text-primary">
      Restaurants
    </h1>
    <div v-if="restaurants.length > 0" class="overflow-x-auto">
      <table class="table">
        <!-- head -->
        <thead>
          <tr>
            <th>ID</th>
            <th>Name</th>
            <th>Contact</th>
            <th>Address</th>
          </tr>
        </thead>
        <tbody>
          <tr class="bg-base-200" v-for="item in restaurants" :key="item.id">
            <th>{{ item.id }}</th>
            <td>{{ item.name }}</td>
            <td>{{ item.contact }}</td>
            <td>{{ item.address }}</td>
            <td>
              <router-link
                :to="'/update/' + item.id"
                class="text-blue-500 underline"
                >Update</router-link
              >
            </td>
            <button
              class="btn btn-error"
              v-on:click="deleteRestaurant(item.id)"
            >
              X
            </button>
          </tr>
          <tr class="bg-base-200"></tr>
        </tbody>
      </table>
    </div>
    <p v-else class="text-xl tracking-wide">
      There are no registered restaurants
    </p>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "Home",

  data() {
    return {
      restaurants: [],
    };
  },

  methods: {
    async deleteRestaurant(id) {
      let result = await axios.delete(
        "http://localhost:3000/restaurants/" + id
      );
      if (result.status === 200) {
        this.loadData();
      }
    },
    async loadData() {
      let user = localStorage.getItem("user-info");
      if (!user) {
        this.$router.push({ name: "Login" });
      }

      let result = await axios.get("http://localhost:3000/restaurants");
      this.restaurants = result.data;
    },
  },

  async mounted() {
    this.loadData();
  },
};
</script>
