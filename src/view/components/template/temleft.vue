<template>
  <div class="template-con">
    <div
      style="
        width: 100%;
        text-align: center;
        margin-bottom: 16px;
        margin-top: 40px;
      "
    >
      <Button
        type="primary"
        icon="ios-add-circle-outline"
        size="large"
        long
        style="height: 50px; width: 232px"
      >
        新建模板
      </Button>
    </div>

    <!-- 新建模板输入框、保存按钮 -->
    <div class="addTeminput">
      <Form ref="formInline" :model="formInline" :rules="ruleInline" inline>
        <FormItem prop="temname">
          <Input
            v-model="formInline.temname"
            placeholder="请输入模板名称..."
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

    <Menu active-name="1" style="width: 100%">
      <div class="tem-menu">
        <MenuItem name="1"> 智能高速五轴 </MenuItem>
        <Button class="btndelete" type="primary"
          ><i class="iconfont icondelete"></i
        ></Button>
      </div>

      <div class="tem-menu">
        <MenuItem name="2"> 高速智能五轴装配 </MenuItem>
        <Button class="btndelete" type="primary"
          ><i class="iconfont icondelete"></i
        ></Button>
      </div>

      <div class="tem-menu">
        <MenuItem name="3"> 五轴机床 </MenuItem>
        <Button class="btndelete" type="primary"
          ><i class="iconfont icondelete"></i
        ></Button>
      </div>

      <div class="tem-menu">
        <MenuItem name="4"> 智能高速五轴 </MenuItem>
        <Button class="btndelete" type="primary"
          ><i class="iconfont icondelete"></i
        ></Button>
      </div>
    </Menu>
  </div>
</template>
<script>
export default {
  data() {
    return {
      // 模板输入，验证
      formInline: {
        temname: "",
      },
      ruleInline: {
        temname: [
          { required: true, message: "模板名称不能为空", trigger: "blur" },
        ],
      },
    };
  },
  methods: {
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
.template-con {
  height: 100%;

  .tem-menu {
    display: flex;
  }
  ::v-deep .ivu-menu,
  .ivu-menu-item {
    font-size: 18px;
    font-weight: bold;
    line-height: 52px;
  }
  .tem-menu .btndelete {
    // float: right;w
    width: 52px;
    height: 52px;
    line-height: 52px;
    text-align: center;
    padding: 0;
    margin-left: 8px;
    background-color: rgba(251, 106, 106, 1);
    border-color: rgba(251, 106, 106, 1);
    display: none;
    .iconfont {
      font-size: 22px !important;
    }
  }
  .addTeminput {
    .ivu-form .ivu-form-item:nth-child(1) {
      width: 256px;
    }
  }
  .ivu-menu-item {
    width: 80%;
  }
  ::v-deep
    .ivu-menu-light.ivu-menu-vertical
    .ivu-menu-item-active:not(.ivu-menu-submenu):after {
    left: 0;
    width: 4px;
  }

  ::v-deep
    .ivu-menu-light.ivu-menu-vertical
    .ivu-menu-item-active:not(.ivu-menu-submenu) {
    background: #e5f1fd;
  }
  ::v-deep .ivu-menu-item-selected + .btndelete {
    display: block;
  }
  ::v-deep .ivu-menu-vertical .ivu-menu-item,
  .ivu-menu-vertical .ivu-menu-submenu-title {
    padding: 0px 24px;
    padding-left: 82px;
  }
  ::v-deep .ivu-menu-vertical.ivu-menu-light:after {
    background: #ffffff;
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
</style>