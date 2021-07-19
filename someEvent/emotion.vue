<template>
  <div class="outerPage">
    <div class="all">
      <span class="manage">Emotion</span>
      <div class="line"></div>
      <span class="detail"
        >Test their feelings so they can deal with them accordingly</span
      >
      <div class="page">
        <div class="innerPage">
          <span class="frontStore">Let's get emotion</span>
          <div class="container">
            <div>
              <div class="crumbs">
                <el-breadcrumb separator="/">
                  <el-breadcrumb-item>
                    <i class="el-icon-lx-cascades"></i>
                  </el-breadcrumb-item>
                </el-breadcrumb>
              </div>
              <div class="emotion">
                <el-table
                  :data="tableData"
                  border
                  class="table"
                  ref="multipleTable"
                  header-cell-class-name="table-header"
                >
                  <el-table-column
                    prop="id"
                    label="编号"
                    align="center"
                    width="50"
                  >
                  </el-table-column>
                  <el-table-column
                    prop="old_person_id"
                    label="老人id"
                    width="70"
                  >
                  </el-table-column>
                  <el-table-column prop="type" label="类型" width="100">
                  </el-table-column>
                  <el-table-column prop="event_date" label="日期" width="300">
                  </el-table-column>
                  <el-table-column
                    prop="event_location"
                    label="地点"
                    width="550"
                  >
                  </el-table-column>
                </el-table>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    const generateData = () => {
      const data = [];
      this.$axios({
        url: "event/emotion",
        method: "get",
        data: {
          type: "Get_emotion_list"
        },

        headers: { "Content-Type": "application/json; charset=utf-8" }
      }).then(res => {
        res.data.forEach(item => {
          data.push({
            id: item.id,
            type: item.type,
            event_date: item.event_date,
            event_location: item.event_location,
            old_person_id: item.old_person_id
          });
        });
      });
      return data;
    };

    return {
      tableData: generateData()
    };
  }
};
</script>

<style lang="scss" scoped>
.outerPage {
  background-color: rgb(220, 245, 215);
  width: 100%;
  height: 1200px;
  margin-top: -80px;
  padding-top: 100px;
  .all {
    background-image: url("../../assets/baidu.jpg");
    margin-left: 200px;
    width: 70%;
    background-size: contain;
    display: flex;
    align-items: center;
    border-radius: 10px;
    .manage {
      position: absolute;
      left: 250px;
      top: 100px;
      font-family: Verdana, Geneva, Tahoma, sans-serif;
      font-size: 60px;
      color: white;
    }
    .line {
      position: absolute;
      left: 500px;
      top: 115px;
      height: 60px;
      width: 2px;
      background-color: white;
    }
    .detail {
      position: absolute;
      left: 530px;
      top: 130px;
      font-family: "Gill Sans", "Gill Sans MT", Calibri, "Trebuchet MS",
        sans-serif;
      font-size: 20px;
      color: white;
    }
    .page {
      margin-top: 95px;
      margin-left: 40px;
      margin-right: 40px;
      margin-bottom: 90px;
      width: 100%;
      background-color: white;
      overflow: hidden;
      border-radius: 10px;
      .innerPage {
        font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto,
          Oxygen, Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
        margin-top: 40px;
        margin-left: 40px;
        margin-right: 40px;
        margin-bottom: 40px;
        background-color: rgb(240, 243, 223);
        border-radius: 10px;
        overflow: hidden;
        .frontStore {
          font-family: or;
          display: inline-block;
          margin-left: 250px;
          margin-top: 30px;
          color: rgb(163, 201, 25);
          font-size: 40px;
        }
        .container {
          margin-top: 60px;
          margin-left: 50px;
          margin-bottom: 50px;
          margin-right: 50px;
        }
      }
    }
  }
}

</style>
