<template>
  <div class="outerPage">
    <div class="all">
      <span class="manage">Interact</span>
      <div class="line"></div>
      <span class="detail"
        >Interact with elders so that they can enjoy themselves</span
      >
      <div class="page">
        <div class="innerPage">
          <span class="frontStore">Interact with elders</span>
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
                  <el-table-column
                    prop="old_person_id"
                    label="老人编号"
                    width="70"
                  >
                  </el-table-column>
                  <el-table-column
                    prop="volunteer_id"
                    label="志愿者编号"
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
        url: "event/interact",
        method: "get",
        data: {
          type: "Get_interact_list"
        },

        headers: { "Content-Type": "application/json; charset=utf-8" }
      }).then(res => {
        res.data.forEach(item => {
          data.push({
            id: item.id,
            type: item.type,
            event_date: item.event_date,
            event_location: item.event_location,
            old_person_id: item.old_person_id,
            volunteer_id: item.volunteer_id
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
@import "../../scss/interact.scss";
</style>
