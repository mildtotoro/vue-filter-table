<template>
  <v-app>
    <v-main>
      <Categories />
    </v-main>
  </v-app>
</template>

<script>
import Categories from "./components/Categories";

export default {
  name: "App",
  components: {
    Categories,
  },
};
</script>
