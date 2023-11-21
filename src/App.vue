<!-- App.vue -->
<template>
  <div class="container mt-5">
    <h1>To-Do List</h1>
    <div class="mt-3">
      <p>Uncompleted Tasks: {{ notCompletedCount }}</p>
    </div>
    <TaskInput @addTask="addTask" />
    <TaskList :tasks="tasks" @editTask="editTask" @toggleCompleted="toggleCompleted" @deleteTask="deleteTask" />
    <EditTaskModal v-if="editedIndex !== null" :title="editedTitle" :content="editedContent" @saveChanges="saveChanges"
      @closeModal="closeModal" />
  </div>
</template>

<script>
import { reactive } from 'vue';
import TaskInput from '@/components/TaskInput.vue';
import TaskList from '@/components/TaskList.vue';
import EditTaskModal from '@/components/base/EditTaskModal.vue';

export default {
  data() {
    return {
      newTask: '',
      tasks: reactive([]),
      editedIndex: null,
      editedTitle: '',
      editedContent: '',
      notCompletedCount: 0,
      completedCount: 0,
    };
  },
  methods: {
    addTask(task) {
      this.tasks.push(task);
      this.updateCounter();
    },
    editTask(index) {
      this.editedIndex = index;
      this.editedTitle = this.tasks[index].title;
      this.editedContent = this.tasks[index].content;
    },
    saveChanges({ title, content }) {
      if (this.editedIndex !== null) {
        this.tasks[this.editedIndex] = { ...this.tasks[this.editedIndex], title, content }
        this.editedIndex = null;
      }
    },
    toggleCompleted(index) {
      this.tasks[index].completed = !this.tasks[index].completed;
      this.updateCounter();
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
      this.updateCounter();
    },
    updateCounter() {
      this.notCompletedCount = this.tasks.filter(task => !task.completed).length;
    },
    closeModal() {
      this.editedIndex = null;
    },
  },
  components: {
    TaskInput,
    TaskList,
    EditTaskModal,
  },
};
</script>
