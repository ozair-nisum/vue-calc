<template>
  <!-- Container div starts -->
  <div class="container w-100">
    <!-- Error div display starts -->
    <div v-show="isError" class="message error">
      <p>{{ errorMessage }}</p>
    </div>
    <!-- Error div display ends -->
    <!-- Input div starts -->
    <div class="input">
      <input
        type="number"
        placeholder="First value"
        @focus="
          () => {
            (isError = false), (result = '');
          }
        "
        v-model="numberOne"
      />
      <input
        type="number"
        placeholder="Second value"
        @focus="
          () => {
            (isError = false), (result = '');
          }
        "
        v-model="numberTwo"
      />
    </div>
    <!-- Input div ends -->
    <!-- Buttons div starts -->
    <div class="buttons col-3">
      <button value="+" @click="operatorClick" :disabled="isDisabled">+</button>
      <button value="-" @click="operatorClick" :disabled="isDisabled">-</button>
      <button value="*" @click="operatorClick" :disabled="isDisabled">*</button>
      <button value="/" @click="operatorClick" :disabled="isDisabled">/</button>
    </div>
    <!-- Buttons div ends -->
    <!-- Loader display starts -->
    <span v-show="isLoading" class="loader" />
    <!-- Loader display ends -->
    <!-- Success display div ends -->
    <div v-show="result" class="message success">
      <p>{{ result }}</p>
    </div>
    <!-- Success display div ends -->
  </div>
  <!-- Container div ends -->
</template>

<script>
export default {
  name: "Calculator",
  data() {
    return {
      numberOne: null,
      numberTwo: null,
      isError: false,
      errorMessage: "Number fields are empty.",
      result: "",
      isLoading: true,
    };
  },
  mounted() {
    this.isLoading = false;
  },
  methods: {
    operatorClick(event) {
      this.result = "";
      if (!this.numberOne || !this.numberTwo) {
        this.isError = true;
        return;
      }
      this.isError = false;
      this.isLoading = true;
      setTimeout(() => {
        this.result = String(
          eval(this.numberOne + event.target.value + this.numberTwo).toFixed(2)
        );
        this.isLoading = false;
      }, 3000);

      return;
    },
  },
  computed: {
    isDisabled() {
      return !this.numberOne || !this.numberTwo;
    },
  },
};
</script>

<style scoped src="./Calculator.css" />
