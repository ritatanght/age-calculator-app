<template>
  <OutputField
    v-for="(output, idx) in outputs"
    :key="idx"
    :value="output.value"
    :unit="output.unit"
  ></OutputField>
</template>

<script>
import OutputField from "./OutputField.vue";
export default {
  name: "OutputList",
  props: ["outputs"],
  components: {
    OutputField,
  },
};
</script>

<style scoped></style>
