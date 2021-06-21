<template>
  <v-container>
    <v-row class="text-center">
      <v-col cols="12">
        <input class="border" type="text" v-model="searchText" />
        <v-list-item-content>
          <v-list-item-title :key="item" v-for="item in filterList">{{
            item
          }}</v-list-item-title>
        </v-list-item-content>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import axios from "axios";

export default {
  name: "Categories",
  data: () => ({
    list: [],
    filterList: [],
    searchText: "",
  }),
  watch: {
    searchText(val) {
      if (val === "") {
        this.filterList = this.list;
      } else {
        const searchVal = val.toLowerCase();
        this.filterList = this.list.filter((item) => {
          return item.toLowerCase().search(searchVal) !== -1;
        });
      }
    },
  },
  async mounted() {
    try {
      const result = await axios.get("https://api.publicapis.org/categories");

      const { data, status } = result;
      if (status === 200) {
        this.list = data;
        this.filterList = data;
      }
    } catch (e) {
      console.error(e);
    }
  },
};
</script>
