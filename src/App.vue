<template>
  <div>
    <div class="display">
      <input @blur="IsNumber" v-model.number="operand1" />
      <input v-model.number="operand2" />
      = {{ result }}
    </div>
    <div class="keyboard">
      <button :disabled="IsNumber" @click="result = operand1 + operand2">
        +
      </button>
      <button :disabled="IsNumber" @click="result = operand1 - operand2">
        -
      </button>
      <button
        :disabled="IsNumber"
        @click="result = operand1 / operand2"
        v-on:click="divisionZero"
      >
        /
      </button>
      <button :disabled="IsNumber" @click="result = operand1 * operand2">
        *
      </button>
      <button :disabled="IsNumber" @click="pow">^</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "Calculator_",
  data() {
    return {
      operand1: 0,
      operand2: 0,
      result: 0,
    };
  },
  methods: {
    pow() {
      this.result = Math.pow(this.operand1, this.operand2);
    },
    divisionZero() {
      if (this.operand2 == 0) {
        this.result = "На ноль делить нельзя";
      }
    },
  },
  computed: {
    IsNumber: function () {
      return this.operand1 % 1 == 0 && this.operand2 % 1 == 0 ? false : true;
    },
  },
};
</script>

<style lang="scss">
.display {
  input {
    font-size: 20px;
    color: black;
    margin-right: 20px;
    padding: 5px;
    border: 1px solid rgb(186, 66, 190);
    border-radius: 5px;
    outline: none;
  }
}

.keyboard {
  display: flex;
  align-items: center;
  margin-top: 25px;
  margin-left: 110px;
  button {
    display: inline-block;
    margin-right: 20px;
    padding: 15px;
    font-size: 25px;
    text-align: center;
    color: white;
    background-color: rgb(186, 66, 190);
    border: 1px solid rgb(186, 66, 190);
    border-radius: 10px;
  }
}
</style>
