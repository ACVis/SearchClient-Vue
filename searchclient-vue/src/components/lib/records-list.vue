<template>
  <div>
    <ul v-if="records && records.hit">
      <record
        class="mb-3"
        v-for="record in records.hit"
        :record="record"
        :key="record.id"
      ></record>
    </ul>
  </div>
</template>

<script>
import dayjs from "dayjs";
import Record from "@/components/lib/record.vue";
const defaultWrapClasses = "";

export default {
  name: "RecordsList",
  components: {
    Record
  },
  filters: {
    toPostDate(inputdate) {
      if (inputdate) {
        return dayjs(inputdate).format("MMMM D, YYYY");
      } else {
        return "";
      }
    }
  },
  props: {
    records: {
      // required: true,
      type: [Object]
    },
    placeholder: {
      type: String
    },
    updating: {
      // default: null,
      type: [String, Boolean]
    },
    wrapClass: {
      type: [String],
      default: () => defaultWrapClasses
    },
    disabled: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {};
  },
  computed: {
    _wrapClass() {
      return this.wrapClass;
    }
  },
  mounted() {},
  methods: {
    truncate(string, limit = 50, postfix = "...") {
      let output = string;

      if (typeof output != "undefined" && output != "") {
        if (output.length > limit) {
          output = output.slice(0, limit) + postfix;
        }
        return output;
      } else {
        return string;
      }
    }
    // dayjs,
    //   search() {
    //     this.$emit("search", this.value, {
    //       search: this.value,
    //       lastSearch: this.lastSearch
    //     });
    //     this.lastSearch = this.value;
    //   }
    // }
  }
};
</script>

<style>
.record-box {
  border-left-color: var(--rorange);
}
</style>
