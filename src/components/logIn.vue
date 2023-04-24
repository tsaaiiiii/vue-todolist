<template>
  <div class="login_page">
    <h1>ONLINE TODO LIST</h1>
    <div class="homepage">
      <div class="illustrate"></div>
      <div>
        <h2>LogIn</h2>

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

        <div class="button">
          <a class="login" @click="login_btn">Login</a>
        </div>
        <div class="signUp">
          <a class="signUpBtn">signUp</a>
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
          password: "",
        },
      },
      token: "",
    };
  },
  methods: {
    login_btn() {
      axios
        .post(`${this.url}/users/sign_in`, this.info)
        .then((res) => {
          console.log(res);
          this.token = res.headers.authorization;
          localStorage.setItem("userToken", this.token);
          alert("LogIn successful！");
          this.info.user.email = "";
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
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
</style>
