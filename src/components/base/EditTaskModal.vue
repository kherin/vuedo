<!-- EditTaskModal.vue -->
<template>
  <div class="modal">
    <!-- ... other modal content ... -->
    <div class="modal-dialog">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title">Edit Task</h5>
        </div>
        <div class="modal-body">
          <div class="mb-3">
            <label for="editedTitle" class="form-label">Title</label>
            <input type="text" class="form-control" v-model="editedTitle" />
          </div>
          <div class="mb-3">
            <label for="editedContent" class="form-label">Content</label>
            <textarea class="form-control" v-model="editedContent"></textarea>
          </div>
        </div>
        <div class="modal-footer">
          <button class="btn btn-primary" @click="saveChanges">Save changes</button>
          <button class="btn btn-secondary" @click="closeModal">Cancel</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['title', 'content'],
  data() {
    return {
      modalVisible: false,
      editedTitle: this.title,
      editedContent: this.content,
    };
  },
  methods: {
    saveChanges() {
      this.$emit('saveChanges', { title: this.editedTitle, content: this.editedContent });
      this.closeModal();
    },
    closeModal() {
      this.modalVisible = false;
      this.$emit('closeModal');
    },
  },
};
</script>

<style scoped>
/* Add your modal styling here */
.modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal-content {
  background-color: white;
  padding: 20px;
  border-radius: 8px;
}

.modal-footer {
  margin-top: 10px;
  text-align: right;
}
</style>
