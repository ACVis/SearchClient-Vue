<template>
    <div>
      <ul v-if="records && records.hit">
        <li class="border mb-3" :key="record.id" v-for="record in records.hit">
          <div class="flex items-start mb-4 text-sm">
                <img :src="record.fields.image_url" class="w-40 h-auto rounded mr-3">
                <div class="flex-1 text-left overflow-auto">
                    <div class="">
                        <span class="font-bold">{{record.fields.post_title}}</span>
                    </div>
                    <div class="">
                        <span class="text-grey text-xs">{{record.fields.author_names}} | </span>
                        <span class="">{{record.fields.post_date | toPostDate}}</span>
                    </div>
                    <p class="text-black leading-normal">{{record.fields.subtitle}}</p>
                    <div class="bg-grey-lighter border border-grey-light text-grey-darkest text-sm font-mono rounded p-3 mt-2 whitespace-pre overflow-auto">{{record.fields.post_excerpt}}</div>
                </div>
            </div>
        </li>
      </ul>
    </div>
</template>

<script>
import dayjs from "dayjs";
const defaultWrapClasses = "";


export default {
  name: "RecordsList",
  filters: {
    toPostDate(inputdate) {
      if(inputdate) {
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
    return {
    };
  },
  computed: {
    _wrapClass() {
      return this.wrapClass;
    }
  },
  mounted() {},
  methods: {
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

<style></style>
