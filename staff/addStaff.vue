<template>
  <div class="outerPage">
    <div class="all">
      <span class="manage">Add</span>
      <div class="line"></div>
      <span class="detail"
        >Add member information so that the database can be updated in real
        time</span
      >
      <div class="page">
        <div class="innerPage">
          <span class="frontStore">Tell us about your information</span>
          <el-form
            ref="addcForm"
            :model="addcForm"
            :rules="rules"
            label-position="left"
            label-width="130px"
            id="selectForm"
          >
            <el-form-item label="name:" prop="name">
              <el-input
                v-model="addcForm.name"
                style="width:65%; margin-right:220px"
              ></el-input>
            </el-form-item>
            <el-input
              v-model="addcForm.x"
              style="position:absolute; top:343px; left:670px;width:60px;margin-left:180px; margin-bottom:10px;"
            ></el-input>
            <el-button
              class="button3"
              type="danger"
              @click="sendPath"
              style="position:absolute; top:343px; left:740px;width:80px;margin-left:180px; margin-bottom:10px;"
              >发请求</el-button
            >
            <el-form-item label="telephone:" prop="tel">
              <el-select
                v-model="query.country"
                placeholder="country"
                class="country"
                style="width:100px;margin-right:15px"
              >
                <el-option key="1" label="+86" value="china"></el-option>
                <el-option key="2" label="+93" value="afghanistan"></el-option>
                <el-option key="3" label="+213" value="algeria"></el-option>
                <el-option key="4" label="+376" value="andorra"></el-option>
                <el-option key="5" label="+1264" value="anguilla"></el-option>
                <el-option key="6" label="+501" value="belize"></el-option>
                <el-option key="7 " label="+61" value="australia"></el-option>
              </el-select>
              <el-input v-model="addcForm.tel" style="width:75% "></el-input>
            </el-form-item>

            <el-form-item label="id_card" prop="id_card">
              <el-input v-model="addcForm.id_card"></el-input>
            </el-form-item>

            <el-form-item label="remarks" prop="mark">
              <el-input
                class="el-input"
                type="textarea"
                :autosize="{ minRows: 8, maxRows: 20 }"
                v-model="addcForm.mark"
              ></el-input>
            </el-form-item>

            <el-form-item>
              <el-row>
                <el-col>
                  <el-button
                    class="button1"
                    type="primary"
                    @click="postContract"
                    >确定</el-button
                  >
                  <el-button
                    class="button2"
                    type="danger"
                    @click="resetContract"
                    >重置</el-button
                  >
                </el-col>
              </el-row>
            </el-form-item>
          </el-form>
        </div>
      </div>
    </div>
  </div>
  <!--    </el-card>-->
</template>

<script>
export default {
  data() {
    return {
      query: {
        country: ""
      },
      addcForm: {
        x: "",
        name: "",
        tel: "",
        id_card: "",
        mark: ""
      },
      nullContract: {
        name: "",
        tel: "",
        id_card: "",
        mark: ""
      },
      rules: {
        name: [
          { required: true, message: "please input name", trigger: "blur" }
        ],
        tel: [{ required: true, message: "please input tel", trigger: "blur" }],
        id_card: [
          { required: true, message: "please input id_card", trigger: "blur" }
        ],
        bank: [
          {
            required: true,
            message: "please input emergency person's name",
            trigger: "blur"
          }
        ],
        account: [
          {
            required: true,
            message: "please input emergency person's tel",
            trigger: "blur"
          }
        ]
      }
    };
  },
  methods: {
    resetContract() {
      this.$confirm("此操作将清空当前信息，是否继续？", "提示", {
        confirmButtonText: "确定",
        cancelButtonText: "取消",
        type: "warning"
      }).then(() => {
        this.addcForm = this.cleanJson(this.addcForm);
        this.$notify({
          title: "成功",
          message: "清空成功！",
          type: "success"
        });
      });
    },
    sendPath() {
      this.$axios({
        url: "/camera/collect",
        method: "post",
        data: {
          path: "rtmp://192.144.218.105/live/" + this.addcForm.x + "_3"
        },

        headers: { "Content-Type": "application/json; charset=utf-8" }
      });
    },
    postContract() {
      this.$refs["addcForm"].validate(valid => {
        if (valid) {
          this.$axios({
            url: "/staff/add",
            method: "post",
            data: {
              username: this.addcForm.name,
              phone: this.addcForm.tel,
              gender: "男",
              checkin_date: "2008-09-01",
              birthday: "1976-02-09",
              id_card: this.addcForm.id_card,
              mark: this.addcForm.mark
            },
            headers: { "Content-Type": "application/json; charset=utf-8" }
          }).then(res => {
            // eslint-disable-next-line no-console
            if (res.status === 200) {
              this.$notify({
                title: "成功",
                message: `添加老人${res.data.msg}基础信息成功！`,
                type: "success"
              });
            }
            console.log(res);
          });
        } else {
          this.$notify({
            title: "失败",
            message: "提交失败！",
            type: "error"
          });
        }
      });
    },
    cleanJson(json) {
      for (let addcFormKey in json) {
        json[addcFormKey] = "";
      }
      return json;
    }
  }
};
</script>

<style lang="scss" scoped>
@import "../../scss/addStaff.scss";
</style>
