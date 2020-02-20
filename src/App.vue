<template>
  <div id="app">
    <input type="text" v-model="text" />
    <h1> {{ decimalNumber }} </h1>
  </div>
</template>

<script>
export default {
  name: "App",
  data: () => {
    return {
      text: undefined,
      binaryText: undefined,
      decimalNumber: 0,
      maxLengthPermit: 50,
    };
  },
  watch: {
    text: function(newVal, oldVal) {
      let isValid = this.isInputValid(newVal);
      
      if (isValid) {        
        this.binaryText = newVal;
        this.calcDecimal();
      } else {
        this.text = oldVal
      }
    }
  },
  methods: {
    calcDecimal() {
      this.decimalNumber = 0
      var total = 0;

      for (let i = this.binaryText.length - 1; i >= 0; i--) {
        let calc = parseInt(this.binaryText[i]) * Math.pow(2, total);
        this.decimalNumber = this.decimalNumber + calc;
        total++;
      }
    },
    isInputValid(text) {
      let typedText = text.charAt(this.text.length - 1);

      if (typedText === "") return true;

      return (
        this.isNumber(typedText) &&
        this.isOneOrZero(typedText) &&
        this.isLengthGreaterThanEigth(text)
      );
    },
    isNumber(number) {
      if (!isNaN(number)) {
        return true;
      } else {
        alert("Not a number!");
      }
    },
    isOneOrZero(number) {
      if (parseInt(number) === 0 || parseInt(number) === 1) {
        return true;
      } else {
        alert("Input must be 0 or 1!");
      }
    },
    isLengthGreaterThanEigth(input) {
      if (input.length > this.maxLengthPermit) {
        alert("Max input exceeded!");
      } else {
        return true;
      }
    }
  }
};
</script>

<style>
</style>
