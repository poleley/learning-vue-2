<template>
  <div class="issue-form-div">
    <form @submit.prevent>
      <my-input
          v-model="formData.title"
          type="text"
          placeholder="Заголовок"
      />
      <div class="textarea-div">
        <my-textarea
            v-model="formData.body"
            placeholder="Дополнительно"
        />
      </div>
      <my-input
          v-model="formData.date"
          type="text"
          placeholder="Срок выполнения"
          onfocus="(this.type='date')"
      />
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
import MyInput from "./UI/MyInput.vue";

export default {
  name: "issue-form",
  components: {MyInput},
  props: {
    issue: {
      type: Object
    }
  },
  methods: {},
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