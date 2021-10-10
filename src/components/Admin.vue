<script>
import axios from "axios";
import Delete from "./Delete.vue";
import Add from "./Add.vue";
import Edit from "./Edit.vue";

export default {
  components: { Delete, Add, Edit },

  data() {
    return {
      users: null,
      isDeleting: false,
      isEditing: false,
      isAdding: false,
      data: null,
      search: "",
    };
  },
  mounted() {
    axios
      .get(
        "https://server-express-oz1ow6qnv-mouldi-souissi.vercel.app/api/users"
      )
      .then((res) => (this.users = res.data))
      .catch((err) => console.log(err));
  },
  methods: {
    toggleDeleting: function(user) {
      this.isDeleting = !this.isDeleting;
      this.data = user;
    },
    toggleEditing: function(user) {
      this.isEditing = !this.isEditing;
      this.data = user;
    },
    toggleAdding: function() {
      this.isAdding = !this.isAdding;
    },
    setData: function(user) {
      this.data = user;
    },
    deleteUser: function() {
      axios
        .delete(
          `https://server-express-oz1ow6qnv-mouldi-souissi.vercel.app/api/users/${this.data._id}`
        )
        .then(() => {
          this.users = this.users.filter((user) => user._id !== this.data._id);
          this.isDeleting = false;
        })
        .catch((err) => console.log(err));
    },
    addUser: function(user) {
      axios
        .post(
          `https://server-express-oz1ow6qnv-mouldi-souissi.vercel.app/api/users`,
          user
        )
        .then((res) => {
          this.users = [...this.users, res.data];
          this.isAdding = false;
        })
        .catch((err) => console.log(err));
    },
    editUser: function(user) {
      axios
        .patch(
          `https://server-express-oz1ow6qnv-mouldi-souissi.vercel.app/api/users/${user._id}`,
          user
        )
        .then((res) => {
          this.users = [
            ...this.users.filter((el) => el._id !== user._id),
            res.data,
          ];
          this.isEditing = false;
        })
        .catch((err) => console.log(err));
    },
  },
};
</script>
<template>
  <div class="container">
    <div class="d-flex align-items-center justify-content-between">
      <h1 class="display-4 my-4">Admin</h1>
      <button class="btn btn-primary" @click="toggleAdding">
        <i class="fa-solid fa-plus me-2"></i>Add user
      </button>
    </div>
    <input
      type="text"
      class="form-control my-5"
      placeholder="Search . . ."
      @change="(e) => (this.search = e.target.value.trim().toLocaleLowerCase())"
    />
    <div v-if="isDeleting">
      <Delete :toggleDeleting="toggleDeleting" :deleteUser="deleteUser" />
    </div>
    <div v-if="isAdding">
      <Add :toggleAdding="toggleAdding" :addUser="addUser" />
    </div>
    <div v-if="isEditing">
      <Edit :toggleEditing="toggleEditing" :data="data" :editUser="editUser" />
    </div>
    <table class="table container">
      <thead>
        <tr>
          <th scope="col">Id</th>
          <th scope="col">Name</th>
          <th scope="col">Email</th>
          <th scope="col">Delete</th>
          <th scope="col">Edit</th>
        </tr>
      </thead>
      <tbody>
        <tr
          v-for="user of users
            .filter(
              (user) =>
                user.name
                  .trim()
                  .toLocaleLowerCase()
                  .includes(search) ||
                user.email
                  .trim()
                  .toLocaleLowerCase()
                  .includes(search) ||
                user._id === Number(search)
            )
            .sort((a, b) => a._id - b._id)"
          :key="user._id"
        >
          <td>{{ user._id }}</td>
          <td>{{ user.name }}</td>
          <td>{{ user.email }}</td>
          <td>
            <button class="btn btn-transparent" @click="toggleDeleting(user)">
              <i class="fa-solid fa-trash-can text-danger"></i>
            </button>
          </td>
          <td>
            <button class="btn btn-transparent" @click="toggleEditing(user)">
              <i class="fa-solid fa-pen-to-square text-warning"></i>
            </button>
          </td>
        </tr>
      </tbody>
    </table>
    <div></div>
  </div>
</template>
