<template>
  <form :class="_wrapClass" @submit.prevent="search()">
    <input
      ref="searchInput"
      :placeholder="placeholder"
      :value="value"
      type="text"
      :class="_inputClass"
      :disabled="disabled"
      @input="$emit('input', $event.target.value)"
    />
    <button :disabled="updating || disabled" :class="_btnClass" type="submit">
      <slot name="spinner">
        <template v-if="updating">
          <i class="fa fa-spinner fa-pulse fa-fw"></i>
          <span class="sr-only">Loading...</span>
        </template>
        <template v-else>Search</template>
      </slot>
    </button>
    <slot></slot>
  </form>
</template>

<script>
const cssClasses = "";
const defaultInputClasses =
  "flex-1 appearance-none bg-gray-200 text-gray-700 border border-gray-200 rounded-l-lg py-3 px-4 leading-tight focus:outline-none focus:bg-white focus:border-orange-500";
const defaultButtonClasses =
  "flex-initial bg-orange-500 hover:bg-orange-700 text-white font-bold tracking-wide py-2 px-4 rounded-r-lg";
const defaultFormClasses = "w-full flex flex-no-wrap items-stretch relative";

export default {
  name: "SimpleSearch",
  props: {
    value: {
      // required: true,
      type: [String]
    },
    placeholder: {
      type: String
    },
    updating: {
      // default: null,
      type: [String, Boolean]
    },
    inputClass: {
      type: [String],
      default: () => defaultInputClasses
    },
    btnClass: {
      type: [String],
      default: () => defaultButtonClasses
    },
    wrapClass: {
      type: [String],
      default: () => defaultFormClasses
    },
    disabled: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {
      searchInput: "",
      lastSearch: ""
    };
  },
  computed: {
    sizeClasses() {
      const classProp = this.classTable;
      if (classProp && classProp.length > 0) {
        return classProp;
      } else {
        return this.defaultTableClasses;
      }
    },
    _inputClass() {
      return (
        this.inputClass +
        (this.big ? ` ${cssClasses.formControlLarge}` : "") +
        (this.small ? ` ${cssClasses.formControlSmall}` : "")
      );
    },
    _btnClass() {
      return (
        this.btnClass +
        (this.big ? ` ${cssClasses.buttonLarge}` : "") +
        (this.small ? ` ${cssClasses.buttonSmall}` : "")
      );
    },
    _wrapClass() {
      return this.wrapClass;
    }
  },
  mounted() {},
  methods: {
    search() {
      this.$emit("search", this.value, {
        search: this.value,
        lastSearch: this.lastSearch
      });
      this.lastSearch = this.value;
    }
  }
};
</script>

<style></style>
