<template>
  <div class="container">
    <div class="contant">
      <nav>
        <ul>
          <li><a href="/login">登入</a></li>
        </ul>
      </nav>
      <div class="register-container">
        <div class="card" ref="registerForm">
          <div class="card-header">註冊頁面</div>
          <div class="card-body">
            <form ref="registerForm">
              <div class="form-group">
                <label for="name">帳號</label>
                <input
                  v-model="registerForm.account"
                  id="name"
                  type="text"
                  class="form-control"
                  name="account"
                  required="required"
                />
              </div>
              
              <div class="form-group">
                <label for="password">密碼</label>
                <input
                  v-model="registerForm.password"
                  id="password"
                  type="password"
                  class="form-control"
                  name="password"
                  required="required"
                />
              </div>
              <div class="form-group">
                <label for="nickname">暱稱</label>
                <input
                  v-model="registerForm.nickname"
                  id="nickname"
                  type="nickname"
                  class="form-control"
                  name="nickname"
                  required="required"
                />
              </div>
              <button
                type="primary"
                class="btn btn-primary"
                @click.prevent="registerUser"
              >
                註冊
              </button>
            </form>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import url from "../router/url"
const appApi = url.api
// var root = 'http://localhost:3050/register'
export default {
  data() {
    return {
      registerForm: {
        account: "",
        password: "",
        nickname: "",
      },
    };
  },
  methods: {
    registerUser() {
      const { account,password,nickname } = this.registerForm
      let params = {
        account,
        password,
        nickname
      };
      if (account == "") {
        alert("請輸入帳號");
        return false;
      }
      if (password == "") {
        alert("請輸入密碼");
        return false;
      }
      axios
        .post( appApi +  "/register", null, { params })
        .then((res) => {
          if (res.data.success) {
            console.log(res);
            alert("註冊成功");
            this.$router.push({ name: "Login" });
          } else {
            this.registerForm.account = "";
            this.registerForm.password = "";
            this.registerForm.nickname = "";
            alert("已有相同使用者名稱");
          }
        });
    },
  },
};
</script>

<style>

.register-container {
  padding-top: 117px;
}
.form-group {
  padding-bottom: 7px;
}
.form-group {
  padding-bottom: 7px;
}
</style>
