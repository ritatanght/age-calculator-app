<script>
import InputField from "./components/InputField.vue";
import OutputList from "./components/OutputList.vue";
export default {
  data() {
    return {
      inputs: [
        { label: "DAY", placeholder: "DD", fieldVal: "", errorMsg: "" },
        { label: "MONTH", placeholder: "MM", fieldVal: "", errorMsg: "" },
        { label: "YEAR", placeholder: "YYYY", fieldVal: "", errorMsg: "" },
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
    OutputList,
  },
  methods: {
    submitForm(event) {
      event.preventDefault();
      // validation of individual field
      this.inputs.forEach((input) => this.validateField(input));

      const errors = this.inputs.filter((item) =>
        Boolean(item.errorMsg)
      ).length;
      if (errors > 0) return;

      // validation of date
      const [day, month, year] = this.inputs.map((input) =>
        Number(input.fieldVal)
      );
      const dateError = this.validateDate([day, month, year]);

      if (dateError) {
        const dayField = this.inputs.find((input) => input.label === "DAY");
        dayField.errorMsg = dateError;
        return;
      }

      // calculate output
      const currentTime = new Date().getTime();
      const birthTime = new Date(year, month - 1, day).getTime();
      let diffInS = (currentTime - birthTime) / 1000;

      const yearAmt = Math.floor(diffInS / (365 * 24 * 60 * 60));
      diffInS -= yearAmt * (365 * 24 * 60 * 60);
      const monthAmt = Math.floor(diffInS / (30 * 24 * 60 * 60));
      diffInS -= monthAmt * (30 * 24 * 60 * 60);
      const dayAmt = Math.floor(diffInS / (24 * 60 * 60));
      this.outputs.forEach((output) => {
        if (output.unit === "years") output.value = yearAmt;
        if (output.unit === "months") output.value = monthAmt;
        if (output.unit === "days") output.value = dayAmt;
      });
    },
    receiveInputChange(inputObj) {
      const { label, value } = inputObj;
      this.inputs.find((input) => input.label === label).fieldVal = value;
    },
    validateField(input) {
      // reset the errorMsg to "" before validation
      input.errorMsg = "";

      // Any field is empty when the form is submitted
      if (!input.fieldVal) input.errorMsg = "This field is required";

      const value = Number(input.fieldVal);
      if (isNaN(value))
        input.errorMsg = `Must be a valid ${input.label.toLowerCase()}`;

      // The day number is not between 1-31
      if (input.label === "DAY" && (value < 0 || value > 31))
        input.errorMsg = "Must be a valid day";

      // The month number is not between 1-12
      if (input.label === "MONTH" && (value < 0 || value > 12))
        input.errorMsg = "Must be a valid month";

      // The year is in the future
      const currentYear = new Date().getFullYear();
      if (input.label === "YEAR" && value > currentYear)
        input.errorMsg = "Must be in the past";
    },
    validateDate(date) {
      const [day, month, year] = date;

      if (month === 2) {
        // calculate if the year is a leap year to determine the valid date
        const isLeapYear =
          year % 4 === 0 || (year % 400 === 0 && year % 100 === 0);
        if ((isLeapYear && day > 29) || (!isLeapYear && day > 28))
          return "Must be a valid date";
      }

      if ([4, 6, 9, 11].includes(month) && day > 30) {
        return "Must be a valid date";
      }

      if (new Date().getTime() < new Date(year, month - 1, day).getTime()) {
        return "Must be in the past";
      }

      return "";
    },
  },
};
</script>

<template>
  <div class="container">
    <form @submit="submitForm">
      <div class="columns">
        <InputField
          v-for="input in inputs"
          :key="input.label"
          :label="input.label"
          :placeholder="input.placeholder"
          :errorMsg="input.errorMsg"
          @input-change="receiveInputChange"
        ></InputField>
      </div>
      <button class="submit-btn" aria-label="submit">
        <img src="/assets/images/icon-arrow.svg" alt="" class="down-arrow" />
      </button>
    </form>
    <div class="output">
      <OutputList :outputs="outputs"></OutputList>
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
  width: 80%;
}

.submit-btn {
  background-color: hsl(259, 100%, 65%);
  border: 0;
  padding: 1.2em;
  border-radius: 50%;
  position: absolute;
  top: 85%;
  right: 0;
  cursor: pointer;
  transition: 0.3s background-color;
}
.submit-btn:hover {
  background-color: hsl(0, 0%, 8%);
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
