<template>
  <button class="button">
    <slot></slot>
  </button>
</template>

<script>
export default {
  name: "my-button"
}
</script>

<style scoped>
.button {
  border-radius: 4px;
  background: transparent;
  font-family: "Roboto", sans-serif;
  font-size: 16px;
  border: none;
}

.button:hover {
  cursor: pointer;
}
</style>