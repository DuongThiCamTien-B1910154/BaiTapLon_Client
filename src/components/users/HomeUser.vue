<template>
  <v-container>
    <!-- <v-col class="pt-5">
      <v-btn color="primary" :to="{ name: 'add-user' }">
        <i class="fas fa-plus"></i> &nbsp;Thêm thành viên
      </v-btn>
    </v-col> -->
    <br/>
    <v-row>
      <v-col cols="auto" class="pt-5 pb-3">
        <v-btn class="pink white--text" :to="{ name: 'add-user' }">
          <i class="fas fa-plus"></i> &nbsp;Thêm thành viên</v-btn
        >
      </v-col>

      <!-- <v-col cols="auto">
        <v-btn color="primary" :to="{ name: 'add-pro' }" >
          <i class="fas fa-plus"></i> &nbsp;Thêm loại sản phẩm</v-btn
        >
      </v-col> -->
    </v-row>
    <!-- <v-btn color="primary" :to="{ name: 'add-pro' }"  class="ma-5">
        <i class="fas fa-plus"></i> &nbsp;Thêm sản phẩm</v-btn
      > -->

    <br />
    <v-alert
      border="left"
      close-text
      dismissible
      dark
      color="green accent-4"
      v-if="show"
    >
      Xóa thành công!
    </v-alert>
    <v-text-field
      v-model="search"
      append-icon="mdi-magnify"
      label="Tìm kiếm (tên)"
      single-line
      hide-details
    >
    </v-text-field>
    <br />
    <!-- <table
    id="contacts"
    class="table table-bordered table-striped"
    style="width: 100%"
    >
      <thead>
        <tr>
          <th>Tên</th>
          <th>Giới tính</th>
          <th>Email</th>
          <th>Actions</th>
        </tr>
      </thead>
      <tbody v-for="user in filteredUser" :key="user._id">
        <tr>
          <td>{{ user.name }}</td>
          <td>{{ user.gender }}</td>
          <td>{{ user.email }}</td>
          <td>
            <router-link :to="{ name: 'edit-user', params: { id: user._id } }"
              ><i class="fa-solid fa-pen-to-square color" color="blue"></i
            ></router-link>
            &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
            <span text @click="removeUser(user._id)"
              ><i class="fa-solid fa-trash-can color" color="red"></i
            ></span>
          </td>
        </tr>
      </tbody>
    </table> -->
    <table
      id="contacts"
      class="table table-bordered table-striped"
      style="width: 100%"
    >
      <thead>
        <tr>
          <th>Tên</th>
          <th>Giới tính</th>
          <th>Email</th>
          <th>Actions</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="user in filteredUser" :key="user._id">
          <td>{{ user.name }}</td>
          <td>{{ user.gender }}</td>
          <td>{{ user.email }}</td>
          <td>
            <router-link :to="{ name: 'edit-user', params: { id: user._id } }"
              ><i class="fa-solid fa-pen-to-square color" color="blue"></i
            ></router-link>
            &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
            <button text @click="removeUser(user._id)">
              <i class="fa-solid fa-trash-can color" color="red"></i>
            </button>
          </td>
        </tr>
      </tbody>
    </table>
  </v-container>
</template>

<script>
import axios from "axios";
import API from "@/services/api.user";
export default {
  name: "HomeUser",
  data() {
    return {
      stt: 1,
      show: false,
      users: [],
      search: "",
    };
  },
  methods: {
    async removeUser(id) {
      console.log(id);
      const res = API.deleteUser(id);
      this.created();
      this.show = true;
    },
    async created() {
      this.users = await API.getAllUser();
      console.log(this.users);
    },
  },

  async mounted() {
    this.created();
    let user = localStorage.getItem("user-info");
    if (!user) {
      this.$router.push({ name: "login" });
    }
  },
  computed: {
    filteredUser: function () {
      return this.users.filter((user) => {
        return user.name.match(this.search);
      });
    },
  },
};
</script>
<style>
.i {
  width: 100px;
  height: 100px;
}
</style>
