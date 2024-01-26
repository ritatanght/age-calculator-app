<template>
  <div>
    <span class="value">{{ value }}</span
    ><span>{{ unit }}</span>
  </div>
</template>

<script>
export default {
  name: "OutputField",
  props: ["value", "unit"],
};
</script>

<style scoped>
div {
  font-size: 5rem;
  font-family: poppins-800i;
  margin-block: -0.3em;
}
span.value {
  letter-spacing: 10px;
  color: hsl(259, 100%, 65%);
}
</style>
