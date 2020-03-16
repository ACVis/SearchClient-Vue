<template>
  <!-- <div :class="classContainer"> -->
  <!-- v-bind:disabled="SelectState.InputDisabled" -->
  <!-- v-bind:class="{
            'Border-green BW-thick': ReasonState.ReadyToSubmit,
        }" -->

  <select
    :value="value"
    class="select-simple mr-5 appearance-none rounded border block appearance-none bg-white border-gray-400 text-base text-gray-700 py-3 px-4 pr-8 leading-tight focus:outline-none focus:bg-white focus:border-orange-500"
    @input="$emit('input', $event.target.value)"
  >
    <option
      v-for="(item, index) in options"
      :key="index"
      :value="item.value"
      :disabled="item.disabled"
      >{{ item.text }}</option
    >
  </select>
  <!-- </div> -->
</template>

<script>
export default {
  name: "select-simple",
  props: {
    value: {
      default: null,
      type: [() => null, String],
    },
    options: {
      default: null,
      type: [Array, Object],
    },
    maxItems: {
      default: 10,
      type: [Number, String],
    },
    classContainer: {
      type: String,
      default: "",
    },
  },
  data() {
    return {
      selected: "",
      defaultTableClasses: "Table Table--rounded",
    };
  },
  computed: {
  },
  watch: {
    data: {
      handler: function() {},
      deep: true,
      immediate: true,
    },
  },
  methods: {},
};
</script>

<style>

</style>
