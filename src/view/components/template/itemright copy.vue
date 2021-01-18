<template>
  <div class="protree-con">
    <div class="teminput">
      <i class="iconfont iconmoban2"></i>
      <span class="temtitle">工序</span>
      <Form ref="formInline" :model="formInline" :rules="ruleInline" inline>
        <FormItem>
          <Input
            v-model="formInline.temname"
            placeholder="请输入工序名称..."
            size="large"
          ></Input>
        </FormItem>

        <FormItem>
          <Button
            type="primary"
            @click="handleSubmit('formInline')"
            size="large"
            >保存</Button
          >
        </FormItem>
      </Form>
    </div>

    <Button
      type="dashed"
      size="large"
      long
      class="btnAddstep"
      icon="md-add"
      @click="addstep()"
      >新增检验项
    </Button>
    <Table
      :columns="tablelist"
      :data="tabledata"
      :show-header="false"
      width="600"
    >
      <template slot-scope="{ row, index }" slot="ind">
        <span style="color: rgba(174, 175, 178, 1)">
          <Badge color="blue" text="" />
          步骤 {{ index + 1 }}</span
        >
      </template>

      <template slot-scope="{ row, index }" slot="action">
        <Button size="small" style="margin-right: 5px" @click="editstep(index)"
          >编辑</Button
        >
        <Button type="error" size="small" @click="remove(index)">删除</Button>
      </template>
    </Table>

    <Modal
      v-model="modal1"
      title="编辑步骤信息"
      @on-ok="ok"
      @on-cancel="cancel"
      ok-text="保存"
      width="620px"
    >
      <Form ref="form" :model="form" label-position="left" :label-width="80">
        <FormItem label="步骤名称" prop="input0">
          <Input
            size="large"
            v-model="form.input0"
            placeholder="请输入步骤名称..."
          ></Input>
        </FormItem>

        <FormItem label="依赖工序" prop="input1">
          <Select v-model="modeltag" filterable multiple size="large">
            <Option
              v-for="item in tagList"
              :value="item.value"
              :key="item.value"
              >{{ item.label }}</Option
            >
          </Select>
        </FormItem>
        <FormItem label="" prop="input2">
          <Input
            v-model="form.input2"
            maxlength="100"
            show-word-limit
            type="textarea"
            placeholder="工序工作内容及注意信息..."
            size="large"
            :rows="4"
          />
        </FormItem>
      </Form>
    </Modal>
  </div>
</template>
<script>
export default {
  data() {
    return {
      modal1: false,
      //步骤标签选择
      modeltag: [],
      tagList: [
        {
          value: "1",
          label: "步骤1",
        },
        {
          value: "2",
          label: "步骤2",
        },
      ], //
      form: {
        input0: "",
        input2: "",
      },
      // 模板输入，验证
      formInline: {
        temname: "",
      },
      ruleInline: {
        temname: [
          { required: true, message: "模板名称不能为空", trigger: "blur" },
        ],
      },
      //
      tablelist: [
        {
          title: "步骤",
          slot: "ind",
          width: 110,
        },
        {
          title: "步骤名称",
          key: "name",
        },
        {
          title: "操作",
          slot: "action",
          width: 130,
        },
      ],
      tabledata: [
        { name: "机床落位" },
        { name: "XZY轴电机安装" },
        { name: "机床几何精度检测" },
        { name: "安装外防护" },
      ],
    };
  },
  methods: {
    // 弹窗
    // 新增步骤
    addstep() {
      //  弹窗
      this.modal1 = true;
      this.form.input0 = "";
      this.modeltag = [];
      this.form.input2 = "";
    },
    // 编辑步骤
    editstep(index) {
      //  弹窗
      this.modal1 = true;
      this.form.input0 = this.tabledata[index].name;
    },
    //
    ok() {
      this.$Message.info("步骤修改成功");
    },
    cancel() {
      this.$Message.info("取消编辑");
    },
    //

    remove(index) {
      this.tabledata.splice(index, 1);
    },

    // 模板输入
    handleSubmit(name) {
      this.$refs[name].validate((valid) => {
        if (valid) {
          this.$Message.success("Success!");
        } else {
          this.$Message.error("Fail!");
        }
      });
    },
  },
};
</script>
<style lang="scss" scoped>
.protree-con {
  height: 100%;

  ::v-deep .ivu-table th,
  ::v-deep .ivu-table td {
    border: none;
  }
  ::v-deep .ivu-table {
    font-size: 16px;
    font-weight: bold;
  }
  ::v-deep .ivu-table:before {
    background-color: #fff;
  }
  .btnAddstep {
    width: 600px;
    margin-top: 4px;
    margin-bottom: 12px;
  }
  ::v-deep .ivu-table .ivu-btn-error {
    background-color: #fb6a6a;
    border-color: #fb6a6a;
  }

  ::v-deep .ivu-table-row-hover td {
    background-color: #e5f1fd;
  }

  .teminput {
    display: flex;
    margin-top: 40px;
    .temtitle {
      font-size: 18px;
      font-weight: bold;
      line-height: 40px;
      margin-left: 8px;
      margin-right: 36px;
    }
    .ivu-form .ivu-form-item:nth-child(1) {
      width: 356px;
    }
  }

  .iconmoban2 {
    background-color: #2d8cf0;
    width: 40px;
    height: 40px;
    border-radius: 6px;
    line-height: 40px;
    text-align: center;
    color: white;
  }
  /*定义滚动条高宽及背景高宽分别对应横竖滚动条的尺寸*/
  ::-webkit-scrollbar {
    width: 3px;
    height: 3px;
    /* // background-color: #2c3e50; */
  }
  /*定义滑块颜色+圆角*/
  ::-webkit-scrollbar-thumb {
    border-radius: 10px;
    background-color: rgba(87, 163, 243, 0);
  }
  /*定义滚动条轨道内阴影+圆角*/
  ::-webkit-scrollbar-track {
    border-radius: 10px;
    background-color: rgba(0, 0, 0, 0);
  }
}
::v-deep .ivu-form .ivu-form-item-label {
  font-size: 16px;
  line-height: 1.3;
}

::v-deep textarea.ivu-input {
  font-size: 16px;
}
</style>