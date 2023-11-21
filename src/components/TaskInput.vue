<!-- TaskInput.vue -->
<template>
    <div class="mb-3">
        <label for="newTask" class="form-label">New Task</label>
        <input type="text" class="form-control" placeholder="Press enter to add item..." v-model="newTask"
            @keyup.enter="addTask" />
    </div>
</template>
  
<script>
export default {
    data() {
        return {
            newTask: '',
        };
    },
    methods: {
        addTask() {
            if (this.newTask.trim() !== '') {
                this.$emit('addTask', { title: this.newTask, completed: false });
                this.newTask = '';
            }
        },
    },
};
</script>
  