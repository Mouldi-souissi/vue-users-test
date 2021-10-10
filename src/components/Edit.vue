<script>
export default {
  props: {
    editUser: { type: Function },
    toggleEditing: { type: Function },
    data: { type: Object },
  },
  data() {
    return {
      name: this.data.name,
      email: this.data.email,
    };
  },
  methods: {
    handleCloseModal: function() {
      this.toggleEditing();
    },
    handleEdit: function() {
      this.editUser({ _id: this.data._id, name: this.name, email: this.email });
    },
  },
};
</script>
<template>
  <div
    class="admin-modal col-8 card p-5 shadow d-flex align-items-center justify-content-center"
  >
    <h4 class="mb-4">Edit User</h4>
    <div class="mb-3">
      <label class="form-label">Name</label>
      <input name="name" type="text" class="form-control" v-model="name" />
    </div>
    <div class="mb-4">
      <label class="form-label">Email</label>
      <input name="email" type="email" class="form-control" v-model="email" />
    </div>

    <div class="d-flex">
      <button class="btn btn-secondary me-2" @click="handleCloseModal">
        cancel
      </button>
      <button class="btn btn-primary" @click="handleEdit">
        Save
      </button>
    </div>
  </div>
</template>
