<template>
  <div>
    <span class="value" v-if="value === '--'">{{ value }}</span
    ><vue3-autocounter
      class="value"
      v-else
      :startAmount="0"
      :endAmount="value"
      :duration="2"
    />
    <span>{{ unit }}</span>
  </div>
</template>

<script>
import Vue3autocounter from "vue3-autocounter";
export default {
  name: "OutputField",
  props: ["value", "unit"],
  components: {
    "vue3-autocounter": Vue3autocounter,
  },
};
</script>

<style scoped>
div {
  font-size: 5rem;
  font-family: poppins-800i;
  margin-block: -0.3em;
}
span.value {
  color: hsl(259, 100%, 65%);
  margin-right: 0.2em;
}

@media screen and (max-width: 500px) {
  div {
    font-size: 3rem;
  }
}
</style>
