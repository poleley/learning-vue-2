<template>
  <div class="button-form-div">
    <my-button
        @click="showCreateDialog"
        class="button-form-create"
    >
      Создать задачу
    </my-button>
    <my-select
        v-model="selectedSort"
        :options="sortOptions"
    >
      Отсортировать...
    </my-select>
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
import MySelect from "./components/UI/MySelect.vue";

export default {
  name: "App",
  components: {MySelect, IssueList, IssueForm},
  mounted() {
    if (localStorage.getItem('issues')) {
      try {
        this.issues = JSON.parse(localStorage.getItem('issues'));
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
        this.selectedSort = "";
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
  watch: {
    selectedSort(newValue) {
      this.issues.sort((i1, i2) => {
        if (newValue === "1") {
          return new Date(i1.date) - new Date(i2.date)
        } else {
          return new Date(i2.date) - new Date(i1.date)
        }
      });
    },
  },
  data() {
    return {
      issues: [
        {
          id: 1,
          title: 'Изучить javascript',
          body: 'Нужно его хорошо изучить',
          completed: false,
          date: "2022-04-11"
        },
        {
          id: 2,
          title: 'Изучить Vue3',
          body: 'Тоже нужно хорошо изучить',
          completed: false,
          date: "2023-04-08"
        }
      ],
      dialogCreateVisibility: false,
      dialogEditVisibility: false,
      editableIssue: null,
      selectedSort: '',
      sortOptions: [
        {name: 'От самого старого к самому новому', value: "1"},
        {name: 'От самого нового к самому старому', value: "2"}
      ]
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
  width: 50%;
  margin: auto;
}

.button-form-create {
  margin: 1rem auto;
  width: 100%;
  padding: 8px 12px;
  background: #50a450 !important;
  color: white;
}


</style>