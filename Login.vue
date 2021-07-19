<template>
  <div class="login">
    <div class="top">
      <span class="companyWord">天网</span>
      <span class="companyEngWord">invisible net</span>
      <a class="a1" @click="chinese()">中文版</a>
      <a class="a2" @click="english()">English</a>
    </div>
    <div class="inBody">
      <div class="runningPic"></div>
      <div class="sheet">
        <span class="loginSpan">管理员登录</span>
        <hr />
        <form>
          <input
            type="text"
            name="name"
            class="name"
            placeholder=" 在此·输入用户名"
            v-model="name"
          />
          <input
            type="text"
            name="password"
            class="password"
            placeholder=" 在此·输入密码"
            v-model="password"
          />
          <input type="submit" name="submit" value="提交" class="submit" @click="postClick()"/>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Login",
  data() {
    return {
      name: "",
      password: ""
    };
  },
  methods: {
    postClick() {
      this.$axios({
        url: "sys_admin/login",
        method: "post",
        data: {
          id: this.name,
          password: this.password,
        },
        headers: { "Content-Type": "application/json; charset=utf-8" }
      }).then(res => {
        console.log(res);
        // eslint-disable-next-line no-console
        if (res.data.code === 200) {
          this.$notify({
            title: "成功",
            message: "登录成功！",
            type: "success"
          });
          this.$router.push("addElder");
        } else {
          this.$notify({
            title: "失败",
            message: "登录失败！",
            type: "error"
          });
        }
      });
    },
    chinese() {
      document.getElementsByClassName("loginSpan")[0].innerHTML = "管理员登录";
      document
        .getElementsByClassName("submit")[0]
        .setAttribute("value", "提交");
      document
        .getElementsByClassName("name")[0]
        .setAttribute("placeholder", " 在此·输入用户名");
      document
        .getElementsByClassName("password")[0]
        .setAttribute("placeholder", " 在此·输入密码");
    },
    english() {
      document.getElementsByClassName("loginSpan")[0].innerHTML = "Admin Login";
      document
        .getElementsByClassName("submit")[0]
        .setAttribute("value", "submit");
      document
        .getElementsByClassName("name")[0]
        .setAttribute("placeholder", " please input your name here");
      document
        .getElementsByClassName("password")[0]
        .setAttribute("placeholder", " please input your password here");
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->

<style lang="scss" scoped>
@import "../scss/login.scss";
</style>
