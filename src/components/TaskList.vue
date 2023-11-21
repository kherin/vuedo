<!-- TaskList.vue -->
<template>
    <ul class="list-group">
        <TaskListItem v-for="(task, index) in tasks" :key="index" :task="task" :index="index" @editTask="editTask"
            @toggleCompleted="toggleCompleted" @deleteTask="deleteTask" />
    </ul>
</template>
  
<script>
import TaskListItem from '@/components/TaskListItem.vue';

export default {
    props: ['tasks'],
    methods: {
        editTask(index) {
            this.$emit('editTask', index);
        },
        toggleCompleted(index) {
            this.$emit('toggleCompleted', index);
        },
        deleteTask(index) {
            this.$emit('deleteTask', index);
        },
    },
    components: {
        TaskListItem,
    },
};
</script>
  