<script>
import InputField from "./components/InputField.vue";
import OutputField from "./components/OutputField.vue";
export default {
  data() {
    return {
      inputs: [
        { label: "DAY", placeholder: "DD", value: "" },
        { label: "MONTH", placeholder: "MM", value: "" },
        { label: "YEAR", placeholder: "YYYY", value: "" },
      ],
      outputs: [
        { value: "--", unit: "years" },
        { value: "--", unit: "months" },
        { value: "--", unit: "days" },
      ],
    };
  },
  components: {
    InputField,
    OutputField,
  },
};
</script>

<template>
  <div class="container">
    <form>
      <div class="columns">
        <InputField
          v-for="input in inputs"
          :key="input.label"
          :label="input.label"
          :placeholder="input.placeholder"
        ></InputField>
      </div>
      <button class="submit-btn" aria-label="submit">
        <img src="/assets/images/icon-arrow.svg" alt="" class="down-arrow" />
      </button>
    </form>
    <div class="output">
      <OutputField
        v-for="(output, idx) in outputs"
        :key="idx"
        :value="output.value"
        :unit="output.unit"
      ></OutputField>
    </div>
  </div>
</template>

<style>
@font-face {
  font-family: poppins-400i;
  src: url("/assets/fonts/Poppins-Italic.ttf");
}

@font-face {
  font-family: poppins-700;
  src: url("/assets/fonts/Poppins-Bold.ttf");
}

@font-face {
  font-family: poppins-800i;
  src: url("/assets/fonts/Poppins-ExtraBoldItalic.ttf");
}

*,
*::before,
*::after {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}
#app {
  background-color: hsl(0, 0%, 94%);
  min-height: 100vh;
  display: grid;
  place-items: center;
}
</style>

<style scoped>
.container {
  background-color: white;
  border-radius: 10px 10px 80px;
  padding: 1.5em;
  max-width: 700px;
}
form {
  font-family: poppins-700;
  border-bottom: 2px solid hsl(0, 0%, 86%);
  position: relative;
  padding-block: 3em;
}

.columns {
  display: flex;
  gap: 5%;
  width: 70%;
}

.submit-btn {
  background-color: hsl(259, 100%, 65%);
  border: 0;
  padding: 1.2em;
  border-radius: 50%;
  position: absolute;
  bottom: -20%;
  right: 0;
  cursor: pointer;
}

.down-arrow {
  max-width: 30px;
}

.output {
  margin-block: 2em;
}

@media screen and (max-width: 500px) {
  .columns {
    width: 100%;
  }
  .submit-btn {
    right: 50%;
    transform: translateX(50%);
  }
  .output {
    margin-top: 4em;
  }

  .container {
    width: 90%;
  }
}
</style>
