<template>
  <div class="outerPage">
    <div class="all">
      <span class="manage">Manage</span>
      <div class="line"></div>
      <span class="detail"
        >Manage their information and maintain the latest version of the
        system</span
      >
      <div class="page">
        <div class="innerPage">
          <span class="frontStore">Let's manage elders</span>
          <div class="container">
            <div class="handle-box">
              <el-select v-model="query.gender" placeholder="sex" class="sex">
                <el-option key="1" label="male" value="male"></el-option>
                <el-option key="2" label="female" value="female"></el-option>
                <el-option key="3" label="" value=""></el-option>
              </el-select>
              <el-input
                v-model="query.name"
                placeholder="name"
                class="name"
              ></el-input>
              <el-button
                class="search"
                type="primary"
                icon="el-icon-search"
                @click="handleSearch"
                >search</el-button
              >
            </div>
            <el-table
              :data="realTable"
              border
              class="table"
              ref="multipleTable"
              header-cell-class-name="table-header"
            >
              <el-table-column
                class="table_head"
                prop="id"
                label="id"
                align="center"
                width="70"
              >
              </el-table-column>
              <el-table-column
                class="table_head"
                prop="name"
                label="name"
                width="90"
              >
              </el-table-column>
              <el-table-column
                class="table_head"
                prop="gender"
                label="gender"
                width="90"
              >
              </el-table-column>
              <el-table-column
                class="table_head"
                prop="birthday"
                label="birthday"
                width="120"
              >
              </el-table-column>
              <el-table-column
                class="table_head"
                prop="phone"
                label="phone"
                width="170"
              >
              </el-table-column>
              <el-table-column
                class="table_head"
                prop="id_card"
                label="id_card"
                width="170"
              >
              </el-table-column>
              <el-table-column class="table_head" label="operation" width="170">
                <template slot-scope="scope">
                  <el-button @click="viewClick(scope.row)" type="text"
                    >view</el-button
                  >
                  <el-dialog
                    title="老年人信息查看"
                    :visible.sync="viewFormVisible"
                  >
                    <el-form :model="viewForm">
                      <el-form-item
                        label="姓名："
                        :label-width="formLabelWidth"
                      >
                        {{ viewForm.name }}
                      </el-form-item>
                      <el-form-item
                        label="性别："
                        :label-width="formLabelWidth"
                      >
                        {{ viewForm.gender }}
                      </el-form-item>
                      <el-form-item
                        label="身份证："
                        :label-width="formLabelWidth"
                      >
                        {{ viewForm.id_card }}
                      </el-form-item>
                      <el-form-item
                        label="电话："
                        :label-width="formLabelWidth"
                      >
                        {{ viewForm.tel }}
                      </el-form-item>
                      <el-form-item
                        label="紧急联系人姓名："
                        :label-width="formLabelWidth"
                      >
                        {{ viewForm.urgent_name }}
                      </el-form-item>
                      <el-form-item
                        label="紧急联系人电话："
                        :label-width="formLabelWidth"
                      >
                        {{ viewForm.urgent_phone }}
                      </el-form-item>
                      <el-form-item
                        label="备注："
                        :label-width="formLabelWidth"
                      >
                        {{ viewForm.mark }}
                      </el-form-item>
                    </el-form>
                    <template #footer>
                      <span class="dialog-footer">
                        <el-button @click="viewFormVisible = false"
                          >关闭</el-button
                        >
                      </span>
                    </template>
                  </el-dialog>
                  <el-button type="text" @click="dialogFormVisible = true"
                    >edit
                  </el-button>
                  <el-dialog
                    title="老年人信息修改"
                    :visible.sync="dialogFormVisible"
                  >
                    <el-form :model="modifyForm">
                      <el-form-item
                        label="身份证"
                        :label-width="formLabelWidth"
                      >
                        <el-input
                          v-model="modifyForm.id_card"
                          autocomplete="off"
                        ></el-input>
                      </el-form-item>
                      <el-form-item label="电话" :label-width="formLabelWidth">
                        <el-input
                          v-model="modifyForm.tel"
                          autocomplete="off"
                        ></el-input>
                      </el-form-item>
                    </el-form>
                    <template #footer>
                      <span class="dialog-footer">
                        <el-button @click="dialogFormVisible = false"
                          >取 消</el-button
                        >
                        <el-button type="primary" @click="postClick(scope.row)"
                          >确 定</el-button
                        >
                      </span>
                    </template>
                  </el-dialog>
                  <el-button
                    class="delete"
                    @click="deleteClick(scope.row)"
                    type="text"
                    >delete</el-button
                  >
                </template>
              </el-table-column>
            </el-table>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "manageElder",

  data() {
    const generateData = () => {
      const data = [];
      this.$axios({
        url: "staff/queryall",
        method: "get",
        data: {
          type: "Get_elder_list"
        },
        headers: { "Content-Type": "application/json; charset=utf-8" }
      }).then(res => {
        if (res.status === 200) {
          this.$notify({
            title: "成功",
            message: "查询成功!",
            type: "success"
          });
        }
        res.data.forEach(item => {
          data.push({
            id: item.id,
            name: item.username,
            age: item.age,
            gender: item.gender,
            birthday: item.birthday,
            phone: item.phone,
            id_card: item.id_card
          });
        });
      });
      return data;
    };

    return {
      dialogFormVisible: false,
      viewFormVisible: false,
      query: {
        gender: "",
        name: ""
      },
      // realTable: generateData(),
      //  tableData: generateData(),
      tableData: generateData(),
      realTable: generateData(),
      formLabelWidth: "140px",
      modifyForm: {
        id_card: "",
        tel: ""
      },
      index: -1,
      row: -1,
      viewForm: {}
    };
  },
  methods: {
    postClick(row) {
      this.dialogFormVisible=false;
      this.$axios({
        url: "staff/modify",
        method: "post",
        data: {
          id_card: this.modifyForm.id_card,
          phone: this.modifyForm.tel,
          id: row.id,
          username: row.name,
          gender: row.gender,
          birthday: row.birthday,
          checkin_date: "2008-09-01"
        },
        headers: { "Content-Type": "application/json; charset=utf-8" }
      }).then(res => {
        // eslint-disable-next-line no-console
        if (res.status === 200) {
          this.$notify({
            title: "成功",
            message: "信息修改成功！",
            type: "success"
          });
        }
        console.log(res);
      });
    },
    handleSearch() {
      let a = [];
      this.tableData.forEach(element => {
        if (this.query.gender === "" && this.query.name === "") {
          a.push(element);
        } else if (
          this.query.name === "" &&
          element.gender === this.query.gender
        ) {
          a.push(element);
        } else if (
          this.query.gender === "" &&
          element.name === this.query.name
        ) {
          a.push(element);
        } else if (
          element.name === this.query.name &&
          element.gender === this.query.gender
        ) {
          a.push(element);
        }
      });
      this.realTable = Object.assign([], a);
    },
    modifyClick(row) {
      this.dialogFormVisible = true;
    },
    viewClick(row) {
      this.$axios({
        url: "/staff/query",
        method: "post",
        data: {
          id: row.id
        },
        headers: { "Content-Type": "application/json; charset=utf-8" }
      }).then(res => {
        // eslint-disable-next-line no-console
        (this.viewForm.name = res.data.username),
          (this.viewForm.tel = res.data.phone),
          (this.viewForm.id_card = res.data.id_card),
          (this.viewForm.urgent_name = res.data.guardian_name),
          (this.viewForm.urgent_phone = res.data.guardian_phone),
          (this.viewForm.mark = res.data.mark),
          (this.viewForm.gender = res.data.gender),
          console.log(res);
      });
      this.viewFormVisible = true;
    },
    deleteClick(row) {
      this.$alert("是否删除该条信息", "DELETE！", {
        confirmButtonText: "确定",
        callback: action => {
          this.$axios({
            url: "staff/delete",
            method: "delete",
            data: {
              type: "Delete_elder",
              id: row.id
            },
            headers: { "Content-Type": "application/json; charset=utf-8" }
          }).then(res => {
            if (res.status === 200) {
              this.$notify({
                title: "成功",
                message: "老人账号注销成功！",
                type: "success"
              });
              console.log(action);
            }
          });
        }
      });
      console.log(row);
    }
  }
};
</script>

<style lang="scss" scoped>
@import "../../scss/manageStaff.scss";
</style>
