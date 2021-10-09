<script>
export default {
  name: "Add",
  props: {
    toggleAdding: { type: Function },
    addUser: { type: Function },
  },
  data() {
    return {
      name: null,
      email: null,
    };
  },

  methods: {
    closeModal: function() {
      this.toggleAdding();
    },

    handleAdd: function() {
      this.addUser({ name: this.name, email: this.email });
    },
  },
};
</script>
<template>
  <div
    class="admin-modal col-8 card p-5 shadow d-flex align-items-center justify-content-center"
  >
    <h4 class="mb-4">Add user</h4>
    <div class="mb-3">
      <label class="form-label">Name</label>
      <input
        name="name"
        type="text"
        class="form-control"
        @change="
          (e) => {
            this.name = e.target.value;
          }
        "
      />
    </div>
    <div class="mb-4">
      <label class="form-label">Email</label>
      <input
        name="email"
        type="email"
        class="form-control"
        @change="
          (e) => {
            this.email = e.target.value;
          }
        "
      />
    </div>
    <div class="d-flex">
      <button class="btn btn-secondary me-2" @click="closeModal">
        cancel
      </button>
      <button class="btn btn-primary" @click="handleAdd">
        Save
      </button>
    </div>
  </div>
</template>
