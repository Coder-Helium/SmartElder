<template>
  <div class="outerPage">
    <div class="all">
      <span class="manage">Setting</span>
      <div class="line"></div>
      <span class="detail">Change the language you like</span>
      <div class="page">
        <div class="innerPage">
          <button @click="back()">注销账户</button>
        </div>
      </div>
    </div>
  </div>
  <!--    </el-card>-->
</template>

<script>
export default {
  data() {
    return { };
  },
  methods: {
    back(){
      window.location.href='/#/'
    }
  }
};
</script>

<style lang="scss" scoped>
@import "../../scss/setting.scss";
</style>
