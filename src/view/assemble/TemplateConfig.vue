<template>
  <div class="app-container temconfig-container">
    <Row class="layRow">
      <!-- 左侧树结构 -->
      <Col span="6" class="leftCol">
        <p class="titleInfo" style="margin-left: 20px; margin-right: 20px">
          <Icon
            type="md-pin"
            style="vertical-align: -0.12em; margin-left: 8px"
          />
          装配模板
        </p>
        <div class="col-d">
          <Itemleft />
        </div>
      </Col>
      <!-- 右侧信息 -->
      <Col span="18" class="rightCol">
        <p class="titleInfo">
          <Icon
            type="md-create"
            style="vertical-align: -0.12em; margin-left: 8px"
          />
          模板详情
        </p>
        <div class="col-d">
          <Itemright />
        </div>
      </Col>
    </Row>
  </div>
</template>
<script>
import Itemleft from "../components/template/itemleft";

import Itemright from "../components/template/itemright";

export default {
  components: {
    Itemleft: Itemleft,
    Itemright: Itemright,
  },
  data() {
    return {};
  },
  methods: {},
};
</script>
<style lang="scss" scoped>
.temconfig-container {
  // 背景处理
  background-color: white;
  border-radius: 20px;
  min-height: 85vh;
  min-width: 1200px;
  // padding-bottom: 20px;

  // 布局
  .layRow {
    // height: 82vh;
    // min-height: 93%;
    min-height: 85vh;
  }
  .col-d {
    height: calc(100% - 85px);
    // overflow-y: auto;
  }
  .leftCol {
    height: 85vh;
    // min-height: 85vh;

    // padding: 0 20px 0 20px;
  }
  .rightCol {
    // border-radius: 20px;
    height: 100%;
    min-height: 85vh;
    padding: 0 20px 20px 20px;
    border-left: 1px solid #dcdfe6;
  }
  .titleInfo {
    font-size: 20px;
    font-weight: bold;
    line-height: 68px;
    color: #555555;
    border-bottom: 1px solid #dcdfe6;
    margin-bottom: 16px;
  }
}
</style>