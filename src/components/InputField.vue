<template>
  <div class="column">
    <label :for="label"> {{ label }}</label>
    <input :placeholder="placeholder" :id="label" />
  </div>
</template>

<script>
export default {
  name: "InputField",
  props: ["label", "placeholder"],
};
</script>

<style scoped>
.column {
  font-family: poppins-700;
  letter-spacing: 2px;
  font-size: 0.7rem;
}
label {
  display: block;
  color: hsl(0, 1%, 44%);
}

input {
  width: 100%;
  font-size: 1.5rem;
  padding: 0.5em;
  margin-block: 0.3em;
  border-radius: 5px;
  border-style: solid;
  border-color: hsl(0, 0%, 86%);
  font-family: poppins-700;
}
input::placeholder {
  color: hsl(0, 0%, 86%);
}
span {
  font-family: poppins-400i;
  color: hsl(0, 100%, 67%);
}
</style>
