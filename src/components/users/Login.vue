<template lang="">
  <v-container>
    <v-alert
      border="left"
      close-text
      dismissible
      dark
      color="red lighten-1"
      v-if="show"
    >
      Email hoặc Mật khẩu chưa đúng!
    </v-alert>
    <v-row justify="center">
      <v-col cols="12" sm="10" md="8" lg="6">
        <v-card>
          <v-card-title
            class="justify-content-center pt-5 bg-primary white--text"
            color="text--darken-2"
            ><h3>Đăng nhập</h3>
          </v-card-title>

          <v-form
            ref="form"
            @submit.prevent="login"
            class="pa-5"
            enctype="multipart/form-data"
          >
            <v-text-field
              v-model="users.email"
              filled
              label="Email"
              :rules="[rules.required]"
            >
            </v-text-field>
            <v-text-field
              v-model="users.password"
              :append-icon="show1 ? 'mdi-eye' : 'mdi-eye-off'"
              :rules="[rules.required, rules.min]"
              :type="show1 ? 'text' : 'password'"
              name="input-10-1"
              label="Mật khẩu"
              hint="At least 8 characters"
              filled
              counter
              @click:append="show1 = !show1"
            ></v-text-field>
            <v-btn type="submit" class="pink white--text float-right"
              >Đăng nhập</v-btn
            >
            <div class="mb-10"></div>
          </v-form>
        </v-card>
        <!-- <v-card>
          <v-card-title class="justify-content-center pt-5 bg-primary white--text"
          color="text--darken-2"  
            >
            <h3>Đăng nhập</h3></v-card-title
          > 
            </v-text-field>
          <v-form>  
            <v-text-field  class="pa-5"
              v-model="users.email"
              label="Email"
              :rules="[rules.required]"
            >
            </v-text-field>
            <v-text-field
            filled
            label="Giá"
            :rules="rules"
          >
          </v-text-field>
            <v-text-field class="pa-5"
              v-model="users.password"
              :append-icon="show1 ? 'mdi-eye' : 'mdi-eye-off'"
              :rules="[rules.required, rules.min]"
              :type="show1 ? 'text' : 'password'"
              name="input-10-1"
              label="Mật khẩu"
              hint="At least 8 characters"
              counter
              @click:append="show1 = !show1"
            ></v-text-field>
            <v-card-actions>
              <v-btn type="submit" class="pink white--text float-right " v-on:click="login">Đăng nhập</v-btn>
            </v-card-actions>
          </v-form>
        </v-card> -->
      </v-col>
    </v-row>
  </v-container>
</template>
<script>
import axios from "axios";
import API from "@/services/api.user";
export default {
  name: "add-user",
  data() {
    return {
      rules: {
        required: (value) => !!value || "This field is Required.",
        min: (v) => v.length >= 8 || "Min 8 characters",
        emailMatch: () => `The email and password you entered don't match`,
      },
      users: {
        email: "",
        password: "",
      },
      show: false,
      show1: false,
    };
  },
  // methods: {
  //   async submitForm() {
  //     const formUser = new FormData();
  //     formUser.append("name", this.users.name);
  //     formUser.append("gender", this.users.gender);
  //     formUser.append("email", this.users.email);
  //     formUser.append("password", this.users.password);
  //     if (this.$refs.form.validate()) {
  //       let result = await API.addUser(formUser);
  //       console.warn(result);

  //       if (result) {
  //         this.show = true;
  //         localStorage.setItem("user-info", JSON.stringify(result));
  //         this.$refs.form.reset();
  //       }
  //     }

  //   },
  // },
  methods: {
    async login() {
      // const formUser = new FormData();
      // formUser.append("email", this.users.email);
      // formUser.append("password", this.users.password);
      if (this.$refs.form.validate()) {
        let result = await API.getLogin(this.users.email, this.users.password);
        console.log(result.status);
        console.warn(result.data.length);
        if (result.status == 200 && result.data.length > 0) {
          console.log(result.data);
          localStorage.setItem("user-info", JSON.stringify(result));
          this.$router.push({ name: "show-product" });
        } else {
          this.show = true;
        }
      }
    },
  },
  // mounted() {
  //   let user = localStorage.getItem("user-info");
  //   if (user) {
  //     this.$router.push({ name: "home" });
  //   }
  // },
};
</script>
<style lang=""></style>
