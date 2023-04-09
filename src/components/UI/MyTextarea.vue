<template>
<textarea
    :value="modelValue"
    @input="updateTextarea"
    class="textarea"
></textarea>
</template>

<script>
export default {
  name: "my-textarea",
  props: {
    modelValue: [String]
  },
  methods: {
    updateTextarea(event) {
      this.$emit('update:modelValue', event.target.value);
    }
  }
}
</script>

<style scoped>
textarea {
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
}

.textarea {
  font-family: "Roboto", sans-serif;
  font-size: 16px;
  width: 100%;
  height: 100%;
  outline: none;
  resize: none;
  padding: 8px;
  border: none;
}

</style>