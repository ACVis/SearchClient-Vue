<template>
  <ul class="pagination ">
    <li class="pagination-item mr-3">
      <button
        type="button"
        class="r-btn-page rounded-l-lg"
        @click="onClickFirstPage"
        :disabled="isInFirstPage"
        aria-label="Go to first page"
      >First</button>
    </li>

    <li class="pagination-item">
      <button
        type="button"
        class="r-btn-page rounded-l-lg"
        @click="onClickPreviousPage"
        :disabled="isInFirstPage"
        aria-label="Go to previous page"
      >Previous</button>
    </li>

    <li v-for="(page, index) in pages" :key="index" class="pagination-item">
      <button
        type="button"
        class="r-btn-page"
        @click="onClickPage(page.name)"
        :disabled="page.isDisabled"
        :class="{ active: isPageActive(page.name) }"
        :aria-label="`Go to page number ${page.name}`"
      >{{ page.name }}</button>
    </li>

    <li class="pagination-item">
      <button
        class="r-btn-page rounded-r-lg"
        type="button"
        @click="onClickNextPage"
        :disabled="isInLastPage"
        aria-label="Go to next page"
      >Next</button>
    </li>
<!-- disable for now -->
    <li class="pagination-item ml-3">
      <button
        type="button"
        class="r-btn-page rounded-r-lg"
        @click="onClickLastPage"
        :disabled="isInLastPage"
        aria-label="Go to last page"
      >Last</button>
    </li>
  </ul>
</template>

<script>
//https://alligator.io/vuejs/vue-pagination-component/
const defaultWrapClasses = "";

export default {
  name: "pagination",
  template: "#pagination",
  props: {
    maxVisibleButtons: {
      type: Number,
      required: false,
      default: 3
    },
    totalPages: {
      type: Number,
      required: true
    },
    total: {
      type: Number,
      required: true
    },
    perPage: {
      type: Number,
      required: true
    },
    currentPage: {
      type: Number,
      required: true
    }
  },
  computed: {
    startPage() {
      if (this.currentPage === 1) {
        return 1;
      }

      if (this.currentPage === this.totalPages) {
        return this.totalPages - this.maxVisibleButtons + 1;
      }

      return this.currentPage - 1;
    },
    endPage() {
      return Math.min(
        this.startPage + this.maxVisibleButtons - 1,
        this.totalPages
      );
    },
    pages() {
      const range = [];

      for (let i = this.startPage; i <= this.endPage; i += 1) {
        range.push({
          name: i,
          isDisabled: i === this.currentPage
        });
      }

      return range;
    },
    isInFirstPage() {
      return this.currentPage === 1;
    },
    isInLastPage() {
      return this.currentPage === this.totalPages;
    }
  },
  methods: {
    onClickFirstPage() {
      this.$emit("pagechanged", 1);
      console.log("first")
    },
    onClickPreviousPage() {
      this.$emit("pagechanged", this.currentPage - 1);
      console.log("prev")
    },
    onClickPage(page) {
      this.$emit("pagechanged", page);
    },
    onClickNextPage() {
      this.$emit("pagechanged", this.currentPage + 1);
    },
    onClickLastPage() {
      this.$emit("pagechanged", this.totalPages);
    },
    isPageActive(page) {
      return this.currentPage === page;
    }
  }
};
</script>

<style>
.record-box {
  border-left-color: var(--rorange);
}
.pagination {
  list-style-type: none;
}

.pagination-item {
  display: inline-block;
}

.active {
  background-color: #4aae9b;
  color: #ffffff;
}

button {
  /* border: none; */
  background: var(--rorange);
  /* color: white; */
}
</style>
