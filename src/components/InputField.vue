<template>
  <div class="column">
    <label :for="label" :class="{ error: errorMsg }"> {{ label }}</label>
    <input
      :placeholder="placeholder"
      :id="label"
      v-model="value"
      @input="onInputChange"
      :class="{ error: errorMsg }"
    />
    <span v-if="errorMsg" class="error">{{ errorMsg }}</span>
  </div>
</template>

<script>
export default {
  name: "InputField",
  props: ["label", "placeholder", "errorMsg"],
  emits: ["input-change"],
  data() {
    return {
      value: "",
    };
  },
  methods: {
    onInputChange() {
      this.$emit("input-change", {
        label: this.label,
        value: this.value,
      });
    },
  },
};
</script>

<style scoped>
.column {
  font-family: poppins-700;
  letter-spacing: 2px;
  font-size: 0.8rem;
  flex-basis: 30%;
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
input:focus {
  outline-color: hsl(259, 100%, 65%);
  caret-color: hsl(259, 100%, 65%);
}

input.error {
  border-width: 2px;
  border-color: hsl(0, 100%, 67%);
}
input::placeholder {
  color: hsl(0, 0%, 86%);
}
span {
  font-family: poppins-400i;
  letter-spacing: 0;
}
.error {
  color: hsl(0, 100%, 67%);
}
@media screen and (max-width: 500px) {
  input {
    font-size: 1.2rem;
  }
}
</style>
