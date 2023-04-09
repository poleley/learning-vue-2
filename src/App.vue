<template>
  <div class="button-form-div">
    <my-button
        @click="showCreateDialog"
        class="button-form-create"
    >
      Создать задачу
    </my-button>
  </div>

  <my-dialog v-model:show="dialogCreateVisibility">
    <template v-slot:title>Создать задачу</template>
    <template v-slot:body>
      <issue-form
          @save="saveIssue"
      />
    </template>
  </my-dialog>

  <my-dialog v-model:show="dialogEditVisibility">
    <template v-slot:title>Редактировать задачу</template>
    <template v-slot:body>
      <issue-form
          :issue="editableIssue"
          @save="saveIssue"
      >
      </issue-form>
    </template>
  </my-dialog>

  <issue-list
      :issues="issues"
      @remove="removeIssue"
      @start-edit="startEditIssue"
      @close="closeIssue"
  />
</template>

<script>
import IssueList from "./components/IssueList.vue";
import IssueForm from "./components/IssueForm.vue";
export default {
  name: "App",
  components: {IssueList, IssueForm},
  mounted() {
    if (localStorage.getItem('issues')) {
      try {
        this.issues = JSON.parse(localStorage.getItem('issues'));
        console.log(this.issues);
      } catch (e) {
        localStorage.removeItem('issues');
      }
    }
  },
  methods: {
    saveIssue(issue) {
      if (this.editableIssue === null) {
        issue.id = Date.now();
        issue.completed = false;
        this.issues.push(issue);
        this.dialogCreateVisibility = false;
      } else {
        this.issues[this.issues.findIndex(i => i.id === this.editableIssue.id)] = issue;
        this.dialogEditVisibility = false;
        this.editableIssue = null;
      }
      this.saveIssues();
    },
    removeIssue(issue) {
      this.issues = this.issues.filter(i => i.id !== issue.id);
      this.saveIssues();
    },
    startEditIssue(issueId) {
      this.dialogEditVisibility = true;
      this.editableIssue = this.issues.find(i => i.id === issueId);
    },
    saveIssues() {
      const parsed = JSON.stringify(this.issues);
      localStorage.setItem('issues', parsed);
    },
    showCreateDialog() {
      this.dialogCreateVisibility = true;
    },
    closeIssue(issueId) {
      this.issues[this.issues.findIndex(i => i.id === issueId)].completed = true;
      this.saveIssues();
    }
  },
  data() {
    return {
      issues: [
        {
          id: 1,
          title: 'Изучить javascript',
          body: 'Нужно его хорошо изучить',
          completed: false
        },
        {
          id: 2,
          title: 'Изучить Vue3',
          body: 'Тоже нужно хорошо изучить',
          completed: false
        }
      ],
      dialogCreateVisibility: false,
      dialogEditVisibility: false,
      editableIssue: null
    }
  }
}
</script>

<style scoped>
* {
  box-sizing: border-box;
  font-family: "Roboto", sans-serif;
  align-content: center;
}

.button-form-div {
  display: flex;
  justify-content: center;
  align-items: center;
}

.button-form-create {
  margin: 1rem auto;
  width: 50%;
  padding: 8px 12px;
  background: #50a450 !important;
  color: white;
}


</style>