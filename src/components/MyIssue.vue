<template>
  <div class="issue" v-bind:class="{'issue-opened': !completed, 'issue-closed': completed}">
    <div class="issue-header">
      <div class="issue-title">{{ title }}</div>
      <div>
        <my-button v-if="completed === false" @click="$emit('edit')">
          <i class="bi bi-pencil"></i>
        </my-button>
        <my-button v-if="completed === false" @click="$emit('close')">
          <i class="bi bi-check-circle"></i>
        </my-button>
        <my-button @click="$emit('remove')">
          <i class="bi bi-trash3 delete"></i>
        </my-button>
      </div>
    </div>
    <div class="issue-text">
      {{ body }}
    </div>
  </div>
</template>

<script>
export default {
  name: "MyIssue",
  props: {
    title: String,
    body: String,
    completed: Boolean
  },
  components: {

  }
}
</script>

<style scoped>
.issue {
  margin: 0 auto 2rem auto;
  padding: 1em;
  border-radius: 8px;
  max-width: 100%;
}

.issue-opened {
  box-shadow: 0 0 14px #50a450;
}

.issue-closed {
  box-shadow: 0 0 14px #676767;
}

.issue-header {
  display: flex;
  justify-content: space-between;
  margin-bottom: 12px;
}

.issue-title {
  font-size: 20px;
  font-weight: bold;
  margin: auto 0;
}

.issue-text {
  word-wrap: break-word;
}
</style>