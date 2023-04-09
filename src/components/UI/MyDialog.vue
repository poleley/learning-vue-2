<template>
  <div class="dialog" v-if="show" @click="hideDialog()">
    <div @click.stop class="dialog-body">
      <div class="my-modal-title">
        <slot name="title"></slot>
      </div>
      <slot name="body"></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: "my-dialog",
  props: {
    show: {
      type: Boolean,
      default: false
    }
  },
  methods: {
    hideDialog() {
      this.$emit('update:show', false)
    }
  }
}
</script>

<style scoped>
.dialog {
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  background: rgba(0, 0, 0, 0.5);
  position: fixed;
  display: flex;
}

.my-modal-title {
  font-size: 24px;
  font-weight: bold;
  margin-bottom: 2rem;
}

.dialog-body {
  margin: auto;
  background: white;
  border-radius: 8px;
  min-height: 50px;
  min-width: 300px;
  padding: 1.5rem;
}
</style>