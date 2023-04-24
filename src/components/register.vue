<template>
  <div class="homepage_all">
    <h1>ONLINE TODO LIST</h1>
    <div class="homepage">
      <div class="illustrate"></div>
      <div>
        <h2>Register</h2>
        <div class="info">
          <label for="nickname">Nickname</label>
          <input
            type="text"
            placeholder="nickname..."
            class="nickname"
            name="nickname"
            v-model="info.user.nickname"
          />
        </div>
        <div class="info">
          <form>
            <label for="email">Email：</label>
            <input
              type="text"
              placeholder="Email..."
              class="email"
              name="email"
              v-model="info.user.email"
            />
            <div class="info">
              <label for="password">Password：</label>
              <input
                type="text"
                placeholder="Password..."
                class="password"
                name="password"
                v-model="info.user.password"
              />
            </div>
          </form>
        </div>

        <div class="signUp">
          <a class="signUpBtn" @click="signUp_btn">signUp</a>
        </div>

        <div class="button">
          <a class="login">Login</a>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },
  data() {
    return {
      url: "https://todoo.5xcamp.us",
      info: {
        user: {
          email: "",
          nickname: "",
          password: "",
        },
      },
    };
  },
  methods: {
    signUp_btn() {
      axios
        .post(`${this.url}/users`, this.info)
        .then((res) => {
          console.log(res);
          alert("Signup successful！");
          this.info.user.email = "";
          this.info.user.nickname = "";
          this.info.user.password = "";
        })
        .catch((err) => {
          console.log(err);
        });
    },
  },
  mounted() {},
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
