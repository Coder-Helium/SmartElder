<template>
  <div>
    <div class="top">
      <span class="companyWord">天网</span>
      <span class="companyEngWord">invisible net</span>
      <a class="a1" @click="chinese()">中文版</a>
      <a class="a2" @click="english()">English</a>
    </div>
    <ul class="son1" hidden>
      <li>
        <router-link to="/setting"
          ><span class="sonWord">系统设置</span></router-link
        >
      </li>
    </ul>
    <ul class="son2" hidden>
      <li>
        <router-link to="/addElder"
          ><span class="sonWord">添加人员</span></router-link
        >
      </li>
      <li>
        <router-link to="/manageElder"
          ><span class="sonWord">管理人员</span></router-link
        >
      </li>
    </ul>
    <ul class="son3" hidden>
      <li>
        <router-link to="/addStaff"
          ><span class="sonWord">添加人员</span></router-link
        >
      </li>
      <li>
        <router-link to="/manageStaff"
          ><span class="sonWord">管理人员</span></router-link
        >
      </li>
    </ul>
    <ul class="son4" hidden>
      <li>
        <router-link to="/addVolunteer"
          ><span class="sonWord">添加角色</span></router-link
        >
      </li>
      <li>
        <router-link to="/manageVolunteer"
          ><span class="sonWord">管理角色</span></router-link
        >
      </li>
    </ul>
    <ul class="son5" hidden>
      <li>
        <router-link to="/elderData"
          ><span class="sonWord">老年人数据分析</span></router-link
        >
      </li>
      <li>
        <router-link to="/staffData">
          <span class="sonWord">工作人员数据分析</span></router-link
        >
      </li>
      <li>
        <router-link to="/volunteerData"
          ><span class="sonWord">义工数据分析</span></router-link
        >
      </li>
    </ul>
    <ul class="son6" hidden>
      <li>
        <router-link to="/emotion"
          ><span class="sonWord">老年人情感检测</span></router-link
        >
      </li>
      <li>
        <router-link to="/falldown">
          <span class="sonWord">老年人摔倒事件</span></router-link
        >
      </li>
      <li>
        <router-link to="/forbid">
          <span class="sonWord">进入禁区事件</span></router-link
        >
      </li>
      <li>
        <router-link to="/interact">
          <span class="sonWord">义工交互事件</span></router-link
        >
      </li>
      <li>
        <router-link to="/interrupt">
          <span class="sonWord">陌生人闯入事件</span></router-link
        >
      </li>
    </ul>
    <ul class="son7" hidden>
      <li>
        <router-link to="/modifyPassword"
          ><span class="sonWord">修改密码</span></router-link
        >
      </li>
      <li>
        <router-link to="/selectCamera1"
          ><span class="sonWord">情感监控</span></router-link
        >
      </li>
      <li>
        <router-link to="/selectCamera2"
          ><span class="sonWord">跌倒监控</span></router-link
        >
      </li>
      <li>
        <router-link to="/selectCamera3"
          ><span class="sonWord">禁区监控</span></router-link
        >
      </li>
      <li>
        <router-link to="/selectCamera4"
          ><span class="sonWord">交互监控</span></router-link
        >
      </li>
    </ul>
    <div id="card" class="card">
      <div id="card1" class="card1">
        <img id="icon1" class="icon" src="../assets/a.jpg" />
      </div>
      <div id="card2" class="card2">
        <img id="icon2" class="icon" src="../assets/lr1.jpg" />
      </div>
      <div id="card3" class="card2">
        <img id="icon3" class="icon" src="../assets/gr.jpg" />
      </div>
      <div id="card4" class="card2">
        <img id="icon4" class="icon" src="../assets/yg.jpg" />
      </div>
      <div id="card5" class="card2">
        <img id="icon5" class="icon" src="../assets/sj.jpg" />
      </div>
      <div id="card6" class="card2">
        <img id="icon6" class="icon" src="../assets/jk.jpg" />
      </div>
      <div id="card7" class="card2">
        <img id="icon7" class="icon" src="../assets/more.jpg" />
      </div>
    </div>
    <div id="t"></div>
    <keep-alive> <router-view class="bodyText"/></keep-alive>
  </div>
</template>

<script>
import * as io from 'socket.io-client';
export default {
  name: "homePage",
  data() {
    return {};
  },
  methods: {}
};
const resizeIcon = n => {
  for (let i = 1; i < 8; i++) {
    if (i === n) {
      continue;
    }
    let r = "icon" + i;
    document.getElementById(r).style.height = "40px";
    document.getElementById(r).style.width = "40px";
  }
};

window.onload = () => {
  window.io = io;
 console.log("qqqqqqqqqqqqqqqqqqqqqqqqq");
  var socket = io.connect(
    "http:" + "//" + "172.27.164.135" + ":" + "8001" + "/dcenter"
  );
  socket.on("dcenter", function(res) {
    var d = res.data;
    var t = res.time;
    console.log(`${d}    ${t}`);
    alert(`${d}    ${t}`);
    //res.time
      
  });

  var card = document.getElementById("card");
  var card1 = document.getElementById("card1");
  var card1_1 = document.getElementById("icon1");
  var card2 = document.getElementById("card2");
  var card2_1 = document.getElementById("icon2");
  var card3 = document.getElementById("card3");
  var card3_1 = document.getElementById("icon3");
  var card4 = document.getElementById("card4");
  var card4_1 = document.getElementById("icon4");
  var card5 = document.getElementById("card5");
  var card5_1 = document.getElementById("icon5");
  var card6 = document.getElementById("card6");
  var card6_1 = document.getElementById("icon6");
  var card7 = document.getElementById("card7");
  var card7_1 = document.getElementById("icon7");

  let length = 0;
  let running = false;
  let open = false;
  let r = 0;
  let s = 0;

  document.addEventListener("mousemove", e => {
    if (e.pageX < 10 && e.pageY > 170 && e.pageY < 840 && !running) {
      clearInterval(s);
      r = setInterval(() => {
        if (length <= 40) {
          length++;
        } else {
          open = true;
          return;
        }
        card.style.width = (length + 3).toString().concat("px");
        card1_1.style.width = length.toString().concat("px");
        card1.style.width = length.toString().concat("px");
        card2_1.style.width = length.toString().concat("px");
        card2.style.width = length.toString().concat("px");
        card3_1.style.width = length.toString().concat("px");
        card3.style.width = length.toString().concat("px");
        card4_1.style.width = length.toString().concat("px");
        card4.style.width = length.toString().concat("px");
        card5_1.style.width = length.toString().concat("px");
        card5.style.width = length.toString().concat("px");
        card6_1.style.width = length.toString().concat("px");
        card6.style.width = length.toString().concat("px");
        card7_1.style.width = length.toString().concat("px");
        card7.style.width = length.toString().concat("px");
      }, 10);
      running = true;
    } else if ((e.pageX > 210 || e.pageY < 170 || e.pageY > 840) && running) {
      clearInterval(r);
      s = setInterval(() => {
        if (length > 0) {
          length = length - 1;
        } else {
          open = false;
        }
        card.style.width = length.toString().concat("px");
        card1.style.width = length.toString().concat("px");
        card1_1.style.width = length.toString().concat("px");
        card2.style.width = length.toString().concat("px");
        card2_1.style.width = length.toString().concat("px");
        card3.style.width = length.toString().concat("px");
        card3_1.style.width = length.toString().concat("px");
        card4.style.width = length.toString().concat("px");
        card4_1.style.width = length.toString().concat("px");
        card5.style.width = length.toString().concat("px");
        card5_1.style.width = length.toString().concat("px");
        card6.style.width = length.toString().concat("px");
        card6_1.style.width = length.toString().concat("px");
        card7.style.width = length.toString().concat("px");
        card7_1.style.width = length.toString().concat("px");
      }, 10);
      running = false;
      document.getElementsByClassName("son1")[0].setAttribute("hidden", true);
      document.getElementsByClassName("son2")[0].setAttribute("hidden", true);
      document.getElementsByClassName("son3")[0].setAttribute("hidden", true);
      document.getElementsByClassName("son4")[0].setAttribute("hidden", true);
      document.getElementsByClassName("son5")[0].setAttribute("hidden", true);
      document.getElementsByClassName("son6")[0].setAttribute("hidden", true);
      document.getElementsByClassName("son7")[0].setAttribute("hidden", true);
    } else if (
      e.pageX >= 0 &&
      e.pageX <= 35 &&
      e.pageY >= 190 &&
      e.pageY <= 231 &&
      running &&
      open
    ) {
      resizeIcon();
      document.getElementById("icon1").style.width = "45px";
      document.getElementById("icon1").style.height = "45px";
      document.getElementsByClassName("son1")[0].removeAttribute("hidden");
      document.getElementsByClassName("son2")[0].setAttribute("hidden", true);
      document.getElementsByClassName("son3")[0].setAttribute("hidden", true);
      document.getElementsByClassName("son4")[0].setAttribute("hidden", true);
      document.getElementsByClassName("son5")[0].setAttribute("hidden", true);
      document.getElementsByClassName("son6")[0].setAttribute("hidden", true);
      document.getElementsByClassName("son7")[0].setAttribute("hidden", true);
    } else if (
      e.pageX >= 0 &&
      e.pageX <= 35 &&
      e.pageY >= 232 &&
      e.pageY <= 274 &&
      running &&
      open
    ) {
      resizeIcon();

      document.getElementById("icon2").style.width = "45px";
      document.getElementById("icon2").style.height = "45px";
      document.getElementsByClassName("son1")[0].setAttribute("hidden", true);
      document.getElementsByClassName("son2")[0].removeAttribute("hidden");
      document.getElementsByClassName("son3")[0].setAttribute("hidden", true);
      document.getElementsByClassName("son4")[0].setAttribute("hidden", true);
      document.getElementsByClassName("son5")[0].setAttribute("hidden", true);
      document.getElementsByClassName("son6")[0].setAttribute("hidden", true);
      document.getElementsByClassName("son7")[0].setAttribute("hidden", true);
    } else if (
      e.pageX >= 0 &&
      e.pageX <= 35 &&
      e.pageY >= 275 &&
      e.pageY <= 316 &&
      running &&
      open
    ) {
      resizeIcon();

      document.getElementById("icon3").style.width = "45px";
      document.getElementById("icon3").style.height = "45px";
      document.getElementsByClassName("son1")[0].setAttribute("hidden", true);
      document.getElementsByClassName("son2")[0].setAttribute("hidden", true);
      document.getElementsByClassName("son3")[0].removeAttribute("hidden");
      document.getElementsByClassName("son4")[0].setAttribute("hidden", true);
      document.getElementsByClassName("son5")[0].setAttribute("hidden", true);
      document.getElementsByClassName("son6")[0].setAttribute("hidden", true);
      document.getElementsByClassName("son7")[0].setAttribute("hidden", true);
    } else if (
      e.pageX >= 0 &&
      e.pageX <= 35 &&
      e.pageY >= 317 &&
      e.pageY <= 358 &&
      running &&
      open
    ) {
      resizeIcon();

      document.getElementById("icon4").style.width = "45px";
      document.getElementById("icon4").style.height = "45px";
      document.getElementsByClassName("son1")[0].setAttribute("hidden", true);
      document.getElementsByClassName("son2")[0].setAttribute("hidden", true);
      document.getElementsByClassName("son3")[0].setAttribute("hidden", true);
      document.getElementsByClassName("son4")[0].removeAttribute("hidden");
      document.getElementsByClassName("son5")[0].setAttribute("hidden", true);
      document.getElementsByClassName("son6")[0].setAttribute("hidden", true);
      document.getElementsByClassName("son7")[0].setAttribute("hidden", true);
    } else if (
      e.pageX >= 0 &&
      e.pageX <= 35 &&
      e.pageY >= 359 &&
      e.pageY <= 400 &&
      running &&
      open
    ) {
      resizeIcon();

      document.getElementById("icon5").style.width = "45px";
      document.getElementById("icon5").style.height = "45px";
      document.getElementsByClassName("son1")[0].setAttribute("hidden", true);
      document.getElementsByClassName("son2")[0].setAttribute("hidden", true);
      document.getElementsByClassName("son3")[0].setAttribute("hidden", true);
      document.getElementsByClassName("son4")[0].setAttribute("hidden", true);
      document.getElementsByClassName("son5")[0].removeAttribute("hidden");
      document.getElementsByClassName("son6")[0].setAttribute("hidden", true);
      document.getElementsByClassName("son7")[0].setAttribute("hidden", true);
    } else if (
      e.pageX >= 0 &&
      e.pageX <= 35 &&
      e.pageY >= 401 &&
      e.pageY <= 442 &&
      running &&
      open
    ) {
      resizeIcon();

      document.getElementById("icon6").style.width = "45px";
      document.getElementById("icon6").style.height = "45px";
      document.getElementsByClassName("son1")[0].setAttribute("hidden", true);
      document.getElementsByClassName("son2")[0].setAttribute("hidden", true);
      document.getElementsByClassName("son3")[0].setAttribute("hidden", true);
      document.getElementsByClassName("son4")[0].setAttribute("hidden", true);
      document.getElementsByClassName("son5")[0].setAttribute("hidden", true);
      document.getElementsByClassName("son6")[0].removeAttribute("hidden");
      document.getElementsByClassName("son7")[0].setAttribute("hidden", true);
    } else if (
      e.pageX >= 0 &&
      e.pageX <= 35 &&
      e.pageY >= 443 &&
      e.pageY <= 484 &&
      running &&
      open
    ) {
      resizeIcon(7);

      document.getElementById("icon7").style.width = "45px";
      document.getElementById("icon7").style.height = "45px";
      document.getElementsByClassName("son1")[0].setAttribute("hidden", true);
      document.getElementsByClassName("son2")[0].setAttribute("hidden", true);
      document.getElementsByClassName("son3")[0].setAttribute("hidden", true);
      document.getElementsByClassName("son4")[0].setAttribute("hidden", true);
      document.getElementsByClassName("son5")[0].setAttribute("hidden", true);
      document.getElementsByClassName("son6")[0].setAttribute("hidden", true);
      document.getElementsByClassName("son7")[0].removeAttribute("hidden");
    }
  });
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->

<style lang="scss" scoped>
@import "../scss/homePage.scss";
</style>
