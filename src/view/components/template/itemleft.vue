<template>
  <div class="protree-con">
    <div
      style="
        width: 100%;
        margin-bottom: 16px;
        padding-left: 20px;
        padding-right: 20px;
      "
    >
      <p style="font-size: 16px; font-weight: bold">选择模板：</p>
      <Select v-model="selemodel" size="large">
        <Option v-for="item in temList" :value="item.value" :key="item.value">{{
          item.label
        }}</Option>
      </Select>
    </div>

    <Menu active-name="1" style="width: 100%">
      <div class="tem-menu">
        <MenuItem name="1"> 机床落位 </MenuItem>
        <Button class="btndelete" type="primary"
          ><i class="iconfont icondelete"></i
        ></Button>
      </div>

      <div class="tem-menu">
        <MenuItem name="2"> XZY轴电机安装 </MenuItem>
        <Button class="btndelete" type="primary"
          ><i class="iconfont icondelete"></i
        ></Button>
      </div>

      <div class="tem-menu">
        <MenuItem name="3"> 机床几何精度检测 </MenuItem>
        <Button class="btndelete" type="primary"
          ><i class="iconfont icondelete"></i
        ></Button>
      </div>

      <div class="tem-menu">
        <MenuItem name="4"> 智能检测及润滑油路 </MenuItem>
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
      temList: [
        { value: "1", label: "智能高速五轴" },
        { value: "2", label: "智能高速五轴222" },
      ],
      selemodel: "",
    };
  },
  methods: {},
};
</script>
<style lang="scss" scoped>
.protree-con {
  height: 100%;

  .tem-menu {
    display: flex;
  }
  .ivu-menu {
    z-index: 0;
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