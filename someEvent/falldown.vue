<template>
  <div class="outerPage">
    <div class="all">
      <span class="manage">Falldown</span>
      <div class="line"></div>
      <span class="detail"
        >Judge if they fall down for rescue</span
      >
      <div class="page">
        <div class="innerPage">
          <span class="frontStore">Let's prevent that</span>
          <div class="container">
            <div>
              <div class="crumbs">
                <el-breadcrumb separator="/">
                  <el-breadcrumb-item>
                    <i class="el-icon-lx-cascades"></i>
                  </el-breadcrumb-item>
                </el-breadcrumb>
              </div>
              <div class="interact">
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
        url: "event/falldown",
        method: "get",
        data: {
          type: "Get_forbid_list"
        },

        headers: { "Content-Type": "application/json; charset=utf-8" }
      }).then(res => {
        res.data.forEach(item => {
          data.push({
            id: item.id,
            event_date: item.event_date,
            event_location: item.event_location
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
@import "../../scss/falldown.scss";
</style>
