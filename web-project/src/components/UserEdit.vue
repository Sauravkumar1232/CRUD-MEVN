<template>
  <!DOCTYPE html>
  <html lang="en">
    <head>
      <meta charset="UTF-8" />
      <meta name="viewport" content="width=device-width, initial-scale=1.0" />
      <title>Document</title>
      <link
        href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css"
        rel="stylesheet"
        integrity="sha384-QWTKZyjpPEjISv5WaRU9OFeRpok6YctnYmDr5pNlyT2bRjXh0JMhjY6hW+ALEwIH"
        crossorigin="anonymous"
      />
    </head>
    <body>
      <h1>Userr Edit</h1>
      <!-- <h1>{{ user }}</h1> -->

      <div class="container">
        <div class="alert bg-success my-3">
          <h4 class="text-center" style="color: red">create account(signup)</h4>
        </div>
      </div>

      <div class="container">
        <div class="row">
          <div class="col"></div>
          <div class="col">
            <!--either get or post-->
            <div class="field my-3">
              <label for="" class="form-label">FirstName: </label>
              <input
                type="text"
                id="firstname"
                class="form-control"
                v-model="user.firstname"
              />
            </div>
            <div class="field my-3">
              <label for="" class="form-label">Lastname:</label>
              <input type="text" class="form-control" v-model="user.Lastname" />
            </div>
            <div class="field my-3">
              <!-- <label for="" class="form-label">mobno:</label>
                <input type="text" class="form-control" v-model="mobno" /> -->
              <div class="field my-3">
                <label for="" class="form-label">email:</label>
                <input type="text" class="form-control" v-model="user.email" />
              </div>
              <div class="field my-3">
                <label for="" class="form-label">password:</label>
                <input
                  type="text"
                  class="form-control"
                  v-model="user.password"
                />
              </div>
              <!-- <div class="field my-3">
                  <label for="" class="form-label">Usertype:</label>
                  <input
                    type="text"
                    class="form-control"
                    name="usertype"
                    placeholder="enter usertype(1-admin,2-normal)"
                  />
                </div> -->
            </div>
            <input
              type="submit"
              value="Edit "
              class="btn btn-info my-3 w-100"
              @click="editUser(user._id)"
            />

            <!-- <input
              type="submit"
              value="All Users"
              class="btn btn-info my-3 w-100"
              @click="allUsers()"
            /> -->
          </div>
          <div class="col"></div>
        </div>
      </div>
    </body>
  </html>
</template>
<script>
import router from "@/router";
import axios from "axios";
import { useRoute } from "vue-router";

export default {
  name: "UserEdit",
  data() {
    return {
      user: {},
      // firstname: "",
      // Lastname: "",
      // //   mobno: "",
      // email: "",
      // password: "",
    };
  },

  created() {
    this.getUserData();
  },
  methods: {
    async editUser(id) {
      let data = {
        firstname: this.user.firstname,
        Lastname: this.user.Lastname,
        password: this.user.password,
        email: this.user.email,
      };

      let result = await axios({
        method: "put",
        url: "http://localhost:3000/user/edit/" + id,
        data: data,
      });
      console.log(result);
      if (result.data.success) {
        router.push({ name: "UserList" });
      }
    },

    async getUserData() {
      const route = useRoute();
      let id = route.params.id;

      console.log(id); //   let id = re;
      let result = await axios({
        method: "get",
        url: "http://localhost:3000/user/forEdit/" + id,
      });
      console.log(result, "fetched user for db");
      this.user = result.data.data;
      // this.firstname = result.data.data.firstname;
      // this.Lastname = result.data.data.Lastname;
      // this.email = result.data.data.email;
      // this.password = result.data.data.password;
    },
  },
};
</script>

<style scoped></style>
