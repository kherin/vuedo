<!-- TaskListItem.vue -->
<template>
    <li class="list-group-item">
        <div class="d-flex justify-content-between align-items-center">
            <div>
                <input type="checkbox" class="mx-2" :checked="task.completed" @change="handleToggleCompleted" />
                <span class="ms-2" :class="{ 'text-decoration-line-through': task.completed }">{{ task.title }}</span>
            </div>
            <div class="d-flex justify-content-space-between">
                <button class="btn btn-sm btn-primary mx-1" @click="editTask">Edit</button>
                <button class="btn btn-sm btn-success mx-1" @click="toggleCompleted">Toggle</button>
                <button class="btn btn-sm btn-danger mx-1" @click="deleteTask">Delete</button>
            </div>
        </div>
    </li>
</template>
  
<script>
export default {
    props: ['task', 'index'],
    methods: {
        editTask() {
            this.$emit('editTask', this.index);
        },
        toggleCompleted() {
            this.$emit('toggleCompleted', this.index);
        },
        deleteTask() {
            this.$emit('deleteTask', this.index);
        },
        handleToggleCompleted(event) {
            this.$emit('toggleCompleted', this.index, event.target.checked);
        },
    },
};
</script>
  