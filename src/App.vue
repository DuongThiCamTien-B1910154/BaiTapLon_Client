<template>
  <!-- <div v-if="show">
    <Login></Login>
  </div> -->
  <v-app id="inspire">
    <template>
      <v-navigation-drawer v-model="drawer" app>
        <v-list-item>
          <v-list-item-content>
            <span class="nav-link logo size pink--text"
              ><i class="fa-solid fa-fan"></i>
              <span class="size">Flower Store</span></span
            >
            <v-list-item-title> </v-list-item-title>
            <v-list-item-subtitle class="ml-5"
              >Copyright&copy;ct449-B1910154</v-list-item-subtitle
            >
          </v-list-item-content>
        </v-list-item>
        <v-divider></v-divider>
        <v-list dense>
          <v-list-item-group color="primary">
            <v-list-item
              v-for="(item, i) in items"
              :key="i"
              :to="item.link"
              link
            >
              <v-list-item-icon>
                <v-icon v-text="item.icon"></v-icon>
              </v-list-item-icon>
              <v-list-item-content>
                <v-list-item-title v-text="item.title"></v-list-item-title>
              </v-list-item-content>
            </v-list-item>
            <v-list-item>
              <v-list-item-icon>
                <v-icon>
                  {{ (icon = "fa-solid fa-right-from-bracket") }}
                  <!-- <font-awesome-icon icon="" /> -->
                </v-icon>
              </v-list-item-icon>
              <v-list-item-content>
                <v-list-item-title @click="logout">Đăng xuất</v-list-item-title>
              </v-list-item-content>
            </v-list-item>
          </v-list-item-group>
        </v-list>
      </v-navigation-drawer>

      <v-app-bar app>
        <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>

        <v-toolbar-title>Application</v-toolbar-title>
      </v-app-bar>
    </template>

    <v-main>
      <router-view></router-view>
    </v-main>
  </v-app>
</template>
<script>
// import Login from "@/views/users/Login.vue";
export default {
  data: () => ({
    drawer: null,
    items: [
      {
        title: "Quản Lý Sản Phẩm",
        icon: "fa-solid fa-fan",
        link: "/show-product",
      },
      {
        title: "Quản Lý Danh Mục",
        icon: "fa-brands fa-buffer",
        link: "/category",
      },
      {
        title: "Quản Lý Thành Viên",
        icon: "fa-solid fa-user",
        link: "/show-user",
      },
    ],
    // show: false,
  }),
  components: {
    // Login,
  },
  methods: {
    logout() {
      localStorage.clear();
      this.$router.push({ name: "login" });
    },
  },
  // async mounted() {
  //   let user = localStorage.getItem("user-info");
  //   if (user) {
  //     this.show = true;
  //   }
  // },
};
</script>
<style>
.size {
  margin-top: 3px;
  font-size: 28px;
  font-weight: bolder;
}
</style>
