<template>
  <div class="issue-form-div">
    <form @submit.prevent>
      <my-input
          v-model="formData.title"
          placeholder="Заголовок"
      ></my-input>
      <div class="textarea-div">
        <my-textarea
            v-model="formData.body"
            placeholder="Дополнительно"
        ></my-textarea>
      </div>
      <div class="button-div">
        <my-button
            @click="$emit('save', formData)"
            class="button-create"
        >
          Сохранить
        </my-button>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  name: "issue-form",
  props: {
    issue: {
      type: Object
    }
  },
  methods: {

  },
  data() {
    return {
      formData: {
        ...this.issue
      }
    }
  },
}
</script>

<style scoped>
.issue-form-div {
  width: 40rem;
  border-radius: 8px;
}

.textarea-div {
  width: 100%;
  height: 8rem;
  margin-bottom: 0.5rem;
}

.button-div {
  text-align: right;
}

.button-create {
  padding: 8px 12px;
  background: #50a450 !important;
  color: white;
}
</style>