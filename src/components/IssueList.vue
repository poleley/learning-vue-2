<template>
  <div class="issues">
    <h2>Все задачи</h2>
    <my-issue
        v-for="issue in issues"
        :title="issue.title"
        :body="issue.body"
        :completed="issue.completed"
        :key="issue.id"
        @remove="$emit('remove', issue)"
        @edit="$emit('start-edit', issue.id)"
        @close="$emit('close', issue.id)"
    >
    </my-issue>
  </div>
</template>

<script>
import MyIssue from "./MyIssue.vue";

export default {
  name: "issue-list",
  components: {MyIssue},
  props: {
    issues: {
      type: Array,
      required: true
    }
  }
}
</script>

<style scoped>
.issues {
  width: 50%;
  margin: 0 auto;
}
</style>