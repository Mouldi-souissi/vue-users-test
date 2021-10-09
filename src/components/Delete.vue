<template>
  <div
    class="admin-modal col-8 card p-5 shadow d-flex align-items-center justify-content-center"
  >
    <h4 class="mb-4">Are you sure you want to delete</h4>
    <div class="d-flex">
      <button class="btn btn-secondary me-2" @click="handleClick">
        No
      </button>
      <button class="btn btn-primary" @click="handleDelete">
        Yes
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "Delete",
  props: {
    toggleDeleting: { type: Function },
    deleteUser: { type: Function },
  },

  methods: {
    handleClick: function() {
      this.toggleDeleting();
    },
    handleDelete: function() {
      this.deleteUser();
    },
  },
};
</script>
