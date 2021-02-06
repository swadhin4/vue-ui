<template>
  <div class="">
    <v-data-table
      :page="page"
      :pageCount="noOfPages"
      :headers="headers"
      :items="users"
      :options.sync="options"
      :server-items-length="totalUsers"
      :loading="loading"
      loading-text="Loading... Please wait"
      class="elevation-1"
    >
      <template v-slot:item.logo="{ item }">
        <img :src="item.logo" style="width: 20%;" />
      </template>
    </v-data-table>
  </div>

</template>
<style>
    .text-start{
      width: 30%;
    }
</style>  
<script>
import axios from "axios";
export default {
  name: "Details",
  data() {
    return {
      page: 1,
      totalUsers: 0,
      noOfPages: 0,
      users: [],
      loading: true,
      options: {},
      headers: [
        { text: "Logo", value: "logo" },
        { text: "Name", value: "name" },
        { text: "SSO", value: "sso" },
        { text: "Amount", value: "amount" }
      ],
    };
  },
  watch: {
    options: {
      handler() {
        this.readDataFromAPI();
      },
    },
    deep: true,
  },
  methods: {
    readDataFromAPI() {
      this.loading = true;
      const { page, itemsPerPage } = this.options;
      console.log("Page Number ", page, itemsPerPage);
      let pageNumber = page - 1;
      axios
        .get(
          "http://localhost:3000/users?size=" +
            itemsPerPage +
            "&page=" +
            pageNumber
        )
        .then((response) => {
          this.loading = false;
          this.users = response.data;
          this.totalUsers = response.data.length;
          this.noOfPages = response.data.noOfPages;
          console.log(response)
        });
    },
  },
  mounted() {
    this.readDataFromAPI();
  },
};
</script>