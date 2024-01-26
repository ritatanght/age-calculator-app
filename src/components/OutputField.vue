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
  color: hsl(259, 100%, 65%);
  margin-right: 0.2em;
}

@media screen and (max-width: 500px) {
  div {
    font-size: 3rem;
  }
}
</style>
