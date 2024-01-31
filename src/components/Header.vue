<template>
  <div class="shadow mb-14 navbar bg-base-300">
    <div class="w-2/3 mx-auto">
      <div class="flex-1">
        <router-link
          to="/"
          class="text-3xl font-bold tracking-widest text-primary"
          >KitchenMax</router-link
        >
      </div>
      <div class="flex-none">
        <ul class="px-1 menu menu-horizontal">
          <li>
            <details>
              <summary>Manage</summary>
              <ul class="p-2 rounded-t-none bg-base-300">
                <li><router-link to="/add">Add restaurant</router-link></li>
              </ul>
            </details>
          </li>
          <li v-if="user == null">
            <router-link to="/login">Login</router-link>
          </li>
          <li v-else>
            <button v-on:click="logout">Logout</button>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Header",

  data() {
    return {
      user: localStorage.getItem("user-info"),
    };
  },

  methods: {
    logout() {
      this.user = null;
      localStorage.removeItem("user-info");
      this.$router.push({ name: "Login" });
    },
  },

  mounted() {
    this.user = localStorage.getItem("user-info");
  },
};
</script>
