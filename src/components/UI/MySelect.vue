<template>
<select
    :value="modelValue"
    @change="changeOption"
    class="select"
>
  <option disabled selected hidden value=""><slot></slot></option>
  <option
      v-for="option in options"
      :key="option.value"
      :value="option.value"
  >
    {{ option.name }}
  </option>
</select>
</template>

<script>
export default {
  name: "my-select",
  props: {
    modelValue: {
      type: String
    },
    options: {
      type: Array,
      default: () => []
    }
  },
  methods: {
    changeOption(event) {
      this.$emit('update:modelValue', event.target.value);
    }
  }
}
</script>

<style scoped>

.select {
  width: 100%;
  font-size: 16px;
  height: 2.5rem;
  border: 2px solid #9f9f9f;
  border-radius: 8px;
}

</style>