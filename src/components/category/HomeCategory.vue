<template>
  <v-container>
    <br />
    <v-row>
      <v-col cols="auto" class="pt-5 pb-3">
        <v-btn class="pink white--text" :to="{ name: 'add-category' }">
          <i class="fas fa-plus"></i> &nbsp;Thêm Loại Sản Phẩm</v-btn
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
    <table
      id="contacts"
      class="table table-bordered table-striped"
      style="width: 100%"
    >
      <thead>
        <tr>
          <th>Tên Loai</th>
          <th>Actions</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="cate in filteredCategory" :key="cate._id">
          <td>{{ cate.name }}</td>

          <td>
            <button text @click="remove(cate._id)">
              <i class="fa-solid fa-trash-can color" color="red"></i>
            </button>
          </td>
        </tr>
      </tbody>
    </table>
    <br />
  </v-container>
</template>

<script>
import axios from "axios";
import API from "@/services/api.category";
// import ProductList from "@/components/product/Product.list.vue";

export default {
  name: "Home",
  data() {
    return {
      search: "",
      show: false,
      category: [],
    };
  },

  methods: {
    async remove(id) {
      console.log(id);
      const res = API.deleteCategory(id);
      this.created();
      this.show = true;
    },
    async created() {
      this.category = await API.getAllCategory();
      console.log(this.category);
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
    filteredCategory: function () {
      return this.category.filter((cate) => {
        return cate.name.match(this.search);
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
