<template>
  <li
    @mouseenter="wrapperhover = true"
    @mouseleave="wrapperhover = false"
    :class="{ 'shadow-md': hasImage && wrapperhover, 'border-l-4 shadow-xs transition-shadow duration-500 ease-in-out': hasImage }"

    class="record-box border-b-0 border-r-0 border-t-0 mb-4  "
  >
    <div class="flex mb-0 text-sm border-r border-gray-400">
      <img v-if="hasImage" :src="record.fields.image_url" class="w-40 h-auto ml-0 mr-0" />
      <div v-else class="w-40 h-auto ml-0 mr-0 border-0"></div>
      <div 
       class="flex flex-1 flex-col items-start text-left overflow-auto border-t pt-2"
       :class="{ 'shadow-md': !hasImage && wrapperhover, 'record-box border-l-4  shadow-xs transition-shadow duration-500 ease-in-out':!hasImage }"
      >
        <a
          :href="'http://' + record.fields.site.replace('_', '.') + record.fields.url"
          target="_blank"
          class="pl-3 pr-3 text-lg font-bold hover:text-blue-500 transition-colors duration-200"
          @mouseenter="titlehover = true"
          @mouseleave="titlehover = false"
        >
          {{truncate(record.fields.post_title, 110)}}
          <i
            :class="{ 'opacity-100': titlehover }"
            class="fa fa-link opacity-0 transition-opacity ease-in duration-300"
            aria-hidden="true"
          ></i>
        </a>

        <p class="pl-3 pr-3 text-black leading-none">{{record.fields.subtitle}}</p>
        <div class="pl-3 pr-3 leading-none mt-1 mb-2">
          <span class="text-grey text-xs">{{record.fields.author_names}} | </span>
          <span class="text-grey text-xs">{{record.fields.post_date | toPostDate}}</span>
        </div>
        <div
          class="w-full pl-3 pr-3 pb-2 bg-grey-lighter border-b border-gray-400 flex-1 text-grey-darkest text-sm"
        >{{truncate(record.fields.post_content, 150)}}</div>
      </div>
    </div>
  </li>
</template>

<script>
import dayjs from "dayjs";
import { isEmpty } from "lodash-es"
const defaultWrapClasses = "";

export default {
  name: "RecordsList",
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
    record: {
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
      titlehover: false,
      wrapperhover: false
    };
  },
  computed: {
    hasImage() {
      return this.record.fields.image_url && !isEmpty(this.record.fields.image_url)
    },
    _wrapClass() {
      return this.wrapClass;
    }
  },
  mounted() {},
  methods: {
    isEmpty,
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
  }
};
</script>

<style>
.record-box {
  border-left-color: var(--rorange);
}
/* not working yet */
.record-box-inset {
  /* box-shadow: inset 0px 0px 0px 10px var(--rorange); */
}
.border-l-3 {
  border-left-width: 3px;;
}
.duration-400 {
  transition-duration: 400ms;
}
</style>
