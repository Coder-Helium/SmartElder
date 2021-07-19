<template>
  <div class="outerPage">
    <div class="all">
      <span class="manage">Staff</span>
      <div class="line"></div>
      <span class="detail"
        >View the data straigtly here and make your decision</span
      >
      <div class="page">
        <div class="innerPage">
          <hr class="secondHr" />
          <hr class="thirdHr" />
          <div id="app" class="whole">
            <schart class="wrapper1" canvasId="canvas1" :options="options1" />
            <div class="next">
              <schart class="wrapper2" canvasId="canvas2" :options="options2" />
              <schart class="wrapper3" canvasId="canvas3" :options="options3" />
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import Schart from "vue-schart";
export default {
  data() {
    const generateData = () => {
      const data = [];
      this.$axios({
        url: "staff/statistics",
        method: "get",
        headers: { "Content-Type": "application/json; charset=utf-8" }
      }).then(res => {
        console.log(res);

        const item = res.data.msg;
        let w = JSON.parse(item);
        console.log(w["1"]);
        data.push(w["5"], w["4"], w["3"], w["2"], w["1"]);
        console.log;
      });
      return data;
    };
    return {
      options1: {
        type: "bar",
        title: {
          text: "年龄统计图"
        },
        bgColor: "#fbfbfb",
        labels: ["31岁以下", "31-41岁", "41-51岁", "51-61岁", "61以上"],
        datasets: [
          {
            label: "人数",
            fillColor: "rgba(241, 49, 74, 0.5)",
            data: generateData()
          }
        ]
      },
      options2: {
        type: "x",
        title: {
          text: "年龄统计图"
        },
        bgColor: "#fbfbfb",
        labels: ["60岁以下", "60~65岁", "65~70岁", "70~75岁", "75~80岁"],
        datasets: [
          {
            fillColor: "white",
            data: generateData()
          }
        ]
      },
      options3: {
        type: "line",
        title: {
          text: "年龄统计图"
        },
        bgColor: "#fbfbfb",
        labels: ["60岁以下", "60~65岁", "65~70岁", "70~75岁", "75~80岁"],
        datasets: [
          {
            label: "人数",
            fillColor: "rgba(241, 49, 74, 0.5)",
            data: generateData()
          }
        ]
      }
    };
  },
  components: {
    Schart
  }
};
</script>

<style lang="scss" scoped>
@import "../../scss/staffData.scss";
</style>
