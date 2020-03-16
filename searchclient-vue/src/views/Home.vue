<template>
  <div class="container mx-auto flex-1 p-4">
    <!-- <img alt="Vue logo" src="../assets/logo.png" /> -->
    <!-- <HelloWorld msg="Welcome to Your Vue.js App" /> -->
    <h1 class="text-4xl mb-5">Search Reason Records</h1>
    <SearchSimple
      class="w-full mb-5"
      v-model.trim="searchInput"
      :updating="submitState.updating"
      :placeholder="'Search for records'"
      :disabled="submitState.updating"
      @search="getRecords({search: searchInput})"
    />
    <records-list :records="records" />
    <pagination
      v-if="!isEmpty(records) && !isEmpty(records.hit)"
      :total-pages="pages"
      :total="recordsFound"
      :per-page="10"
      :current-page="currentPage"
      @pagechanged="onPageChange"
    />
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from "@/components/HelloWorld.vue";
import SearchSimple from "@/components/lib/search-simple.vue";
import RecordsList from "@/components/lib/records-list.vue";
import Pagination from "@/components/lib/pagination.vue";
import axios from "axios";
import { isEmpty } from "lodash-es"

const api = axios.create({
  // baseURL: "https://kvkbud4a7i.execute-api.us-west-2.amazonaws.com/production",
  baseURL: "http://localhost:8080/production",
  headers: {
    // "access-control-allow-origin": "*",
    "Access-Control-Allow-Origin": "*",
    "content-type": "application/json"
  }
});

export default {
  name: "Home",
  components: {
    // HelloWorld,
    SearchSimple,
    RecordsList,
    Pagination
  },
  data() {
    return {
      // sortType: "Default",
      // sortOptions:
      searchInput: "",
      lastSearch: "",
      skip: 0,
      take: 10,
      submitState: {
        updating: false
      },
      records: null
    };
  },
  mount() {
    // this.$on("pagechanged", () => {
    //   })
  },
  computed: {
    recordsFound() {
      return !isEmpty(this.records) && this.records.found ? this.records.found : 0;
    },
    pages() {
      return Math.floor(this.recordsFound / this.take);
    },
    currentPage() {
      const page = Math.max(1, this.skip / this.take);
      return page;
    }
  },
  methods: {
    isEmpty,
    onPageChange(input) {
      this.skip = this.take * input;
      this.getRecords({search: this.lastSearch});
    },
    getRecords(params) {
      const search = params?.search;
      this.searchInput = search;
      this.submitState.updating = true;
      // const take = params?.take;
      // const skip = params?.skip;

      // return api.get(`q?=${search}&take=${take}&skip=${skip}`).then(response => {
        // return api.get(`q?=${search}`).then(response => {
          return axios
        .get(`/production/?q=${search}&size=${this.take}&start=${this.skip}`)
        .then(response => {
          this.submitState.updating = false;
          this.records = response.data.hits;
          this.lastSearch = search;
          return response;
        })
        .catch(error => console.log(error));
    }
  }
};
</script>
