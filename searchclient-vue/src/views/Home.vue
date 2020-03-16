<template>
  <div class="container mx-auto flex-1 p-4">
    <h1 class="text-4xl font-medium mb-5 text-blue-900">Search Articles</h1>
    <div class="flex items-end mb-5">
      <label for="sort" class="align-left flex flex-col text-gray-600 text-xs">
        Sort
        <select-simple
          name="sort"
          v-model="sortType"          
          :options="sortOptions"
          :disabled="submitState.updating || skip >= take"
        />
      </label>
    <div class="flex-1">

    <SearchSimple
      class="w-full "
      v-model.trim="searchInput"
      :updating="submitState.updating"
      :placeholder="'Search for records'"
      :disabled="submitState.updating"
      @search="getRecords({search: searchInput})"
    />
</div>
    </div>
    <records-list :records="records" />
    <pagination
      v-if="!isEmpty(records) && !isEmpty(records.hit)"
      :total-pages="pages < 1000 ? pages : 1000"
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
import SelectSimple from "@/components/lib/select-simple.vue";
import RecordsList from "@/components/lib/records-list.vue";
import Pagination from "@/components/lib/pagination.vue";
import axios from "axios";
import { isEmpty, get } from "lodash-es"

const api = axios.create({
  // baseURL: "https://kvkbud4a7i.execute-api.us-west-2.amazonaws.com/production",
  baseURL: "http://localhost:8080/production",
  headers: {
    // "access-control-allow-origin": "*",
    "Access-Control-Allow-Origin": "*",
    "content-type": "application/json"
  }
});

const sortOptions = [
  { text: "Default", value: "", disabled: false },
  { text: "Date - Desc", value: "&sort=post_date+desc", disabled: false },
  { text: "Date - Asc", value: "&sort=post_date+asc", disabled: false },
];

export default {
  name: "Home",
  components: {
    // HelloWorld,
    SearchSimple,
    SelectSimple,
    RecordsList,
    Pagination
  },
  data() {
    return {
      sortType: "",
      sortOptions: sortOptions,
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
      return Math.ceil(this.recordsFound / this.take);
    },
    currentPage() {
      const page = Math.max(1, (this.skip / this.take) + 1 );
      return page;
    }
  },
  methods: {
    isEmpty,
    onPageChange(input) {
      this.skip = Math.max(0, (this.take * input) - 10);
      this.getRecords({search: this.lastSearch});
    },
    getRecords(params) {
      const search = params?.search;
      this.searchInput = search;
      this.submitState.updating = true;
      // const take = params?.take;
      // const skip = params?.skip;\

      //template literals mess with sourcemap, so we'll do regular concatanation
      const url = "/production/?q=" + search + "&size=" + this.take + "&start=" + this.skip + this.sortType;
      return axios
        .get(url)
        .then(response => {
          this.submitState.updating = false;

          const hits = get(response, "data.hits", null);
          this.records = hits;

          //If new search, reset the skip
          if(search !== this.lastSearch) {
            this.skip = 0;
          }
          //if no results, reset search form
          if(hits === null) {
            this.skip = 0;
            this.lastSearch = "";
            this.searchInput = "";
          } else {
            this.lastSearch = search;
          }
          return response;
        })
        .catch(error => console.log(error));
    }
  }
};
</script>
