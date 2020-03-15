<template>
  <div class="container mx-auto p-4 bg-blue-100">
    <!-- <img alt="Vue logo" src="../assets/logo.png" /> -->
    <!-- <HelloWorld msg="Welcome to Your Vue.js App" /> -->
    <SearchSimple
      class="w-full"
      v-model.trim="searchInput"
      :updating="submitState.updating"
      :placeholder="'Search for records'"
      :disabled="submitState.updating"
      @search="getRecords({search: searchInput})"
    />
    <records-list :records="records" />
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from "@/components/HelloWorld.vue";
import SearchSimple from "@/components/lib/search-simple.vue";
import RecordsList from "@/components/lib/records-list.vue";
import axios from "axios";

const api = axios.create({
  // baseURL: "https://kvkbud4a7i.execute-api.us-west-2.amazonaws.com/production",
  baseURL: "http://localhost:8080/production",
  headers: {
    // "access-control-allow-origin": "*",
    'Access-Control-Allow-Origin': '*',
    "content-type": "application/json",
  }
});

export default {
  name: "Home",
  components: {
    // HelloWorld,
    SearchSimple,
    RecordsList
  },
  data() {
    return {
      // sortType: "Default",
      // sortOptions:
      searchInput: "",
      skip: 0,
      take: 25,
      lastSearch: "",
      submitState: {
        updating: false
      },
      records: null,
    };
  },
  methods: {
    getRecords(params) {
      const search = params?.search;
      const take = params?.take;
      const skip = params?.skip;

      // return api.get(`q?=${search}&take=${take}&skip=${skip}`).then(response => {
      // return api.get(`q?=${search}`).then(response => {
      return axios.get(`/production/?q=${search}`).then(response => {
        this.records = response.data.hits;
        return response;
      }).catch(error => console.log(error));
    }
  }
};
</script>
