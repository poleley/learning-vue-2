<template>
  <input
      :value="modelValue"
      @input="updateInput"
      class="input"
  >
</template>

<script>
export default {
  name: "my-input",
  props: {
    modelValue: [String, Number]
  },
  methods: {
    updateInput(event) {
      this.$emit('update:modelValue', event.target.value);
    }
  }
}
</script>

<style scoped>
.input {
  width: 100%;
  height: 3rem;
  font-size: 20px;
  padding: 8px;
  margin-bottom: 1rem;
  outline: none;
  border: none;
  border-bottom: 1px solid #939393;
}

input {
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
}
</style>