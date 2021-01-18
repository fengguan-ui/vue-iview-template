<template>
  <div class="app-container machineData-container">
    <!-- 检索区 -->

    <div class="searchArea">
      <Form :model="formItem" :label-width="120" inline>
        <Row>
          <Col span="8">
            <FormItem label="机床编号">
              <Input
                v-model="formItem.input0"
                placeholder="请输入机床编号..."
                size="large"
              ></Input>
            </FormItem>
          </Col>
          <Col span="8">
            <FormItem label="检验项目">
              <Input
                v-model="formItem.input1"
                placeholder="请输入检验项目进行搜索..."
                size="large"
              ></Input>
            </FormItem>
          </Col>
          <Col span="8">
            <FormItem label="检测值">
              <Input
                v-model="formItem.input2"
                placeholder="请输入检测值进行搜索..."
                size="large"
              ></Input>
            </FormItem>
          </Col>

          <FormItem label="">
            <Button type="primary" size="large">查询</Button>
            <Button size="large" style="margin-left: 10px">重置</Button>
          </FormItem>
        </Row>
      </Form>
    </div>

    <div class="tablecon">
      <Table :columns="columns1" :data="data1">
        <!-- 检测值状态 -->
        <template slot-scope="{ row, index }" slot="state">
          <Tag
            :color="
              row.state == '自检通过'
                ? 'green'
                : row.state == '自检未通过'
                ? 'red'
                : row.state == '专检通过'
                ? 'green'
                : row.state == '专检未通过'
                ? 'red'
                : row.state == '终检通过'
                ? 'green'
                : row.state == '终检不通过'
                ? 'red'
                : row.state == '已覆盖'
                ? 'purple'
                : 'default'
            "
          >
            {{ row.state }}
          </Tag>
        </template>

        <!-- 覆盖来源 -->
        <template slot-scope="{ row, index }" slot="source">
          <Tag
            :color="
              row.source == '自检通过'
                ? 'green'
                : row.source == '自检未通过'
                ? 'red'
                : row.source == '专检通过'
                ? 'green'
                : row.source == '专检未通过'
                ? 'red'
                : row.source == '终检通过'
                ? 'green'
                : row.source == '终检不通过'
                ? 'red'
                : 'default'
            "
          >
            {{ row.source }}
          </Tag>
        </template>
      </Table>

      <div class="tabpage">
        <Page :total="100" show-sizer />
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      // 表单

      formItem: {
        input0: "",
        input1: "",
        input2: "",
      },

      // 表格
      columns1: [
        {
          title: "机床编号",
          key: "No",
        },
        {
          title: "检验项目",
          key: "item",
        },
        {
          title: "检测值",
          key: "count",
        },
        {
          title: "检测值状态",
          slot: "state",
        },
        {
          title: "覆盖来源",
          slot: "source",
        },
        {
          title: "操作人",
          key: "operator",
        },
      ],
      data1: [
        {
          No: "J8230",
          item: "X联轴器径向跳动",
          count: "0.01",
          state: "自检通过",
          source: "自检通过",
          operator: "张三",
        },
        {
          No: "J8230",
          item: "X联轴器径向跳动",
          count: "0.01",
          state: "自检未通过",
          source: "自检未通过",
          operator: "张三",
        },
        {
          No: "J8230",
          item: "X联轴器径向跳动",
          count: "0.01",
          state: "专检通过",
          source: "专检通过",
          operator: "张三",
        },
        {
          No: "J8230",
          item: "X联轴器径向跳动",
          count: "0.01",
          state: "专检未通过",
          source: "专检未通过",
          operator: "张三",
        },
        {
          No: "J8230",
          item: "X联轴器径向跳动",
          count: "0.01",
          state: "未检测",
          source: "未检测",
          operator: "张三",
        },
        {
          No: "J8230",
          item: "X联轴器径向跳动",
          count: "0.01",
          state: "终检不通过",
          source: "终检不通过",
          operator: "张三",
        },
        {
          No: "J8230",
          item: "X联轴器径向跳动",
          count: "0.01",
          state: "终检通过",
          source: "终检通过",
          operator: "张三",
        },
        {
          No: "J8230",
          item: "X联轴器径向跳动",
          count: "0.01",
          state: "已覆盖",
          source: "自检通过",
          operator: "张三",
        },
      ],
    };
  },
  methods: {},
};
</script>
<style lang="scss" scoped>
.machineData-container {
  // 背景处理
  //   background-color: white;
  //   border-radius: 20px;
  min-height: 85vh;
  min-width: 1200px;

  .searchArea {
    border-radius: 20px;
    background: white;
    margin-bottom: 16px;
    border-radius: 10px;
    margin-top: 16px;
    box-shadow: 0px 0px 10px 0px rgba(74, 82, 96, 0.38);
    padding: 20px 20px 10px 20px;

    ::v-deep .ivu-form-inline .ivu-form-item {
      width: 100%;
      margin-bottom: 10px;
    }
    ::v-deep .ivu-input,
    .ivu-select,
    .ivu-date-picker {
      width: 100%;
    }
    ::v-deep .ivu-form .ivu-form-item-label {
      font-size: 16px;
      line-height: 1.3;
    }
    ::v-deep .ivu-checkbox-wrapper {
      font-size: 15px;
    }
    ::v-deep .ivu-checkbox-large.ivu-checkbox-border,
    .ivu-checkbox-group.ivu-checkbox-large .ivu-checkbox-border {
      line-height: 38px;
    }
  }
  .tablecon {
    // min-height: calc(85vh - 200px);
    border-radius: 20px;
    // background: rgb(255, 255, 255);
    margin-bottom: 16px;
    border-radius: 10px;
    .ivu-tag {
      font-size: 15px;
      height: 32px;
      line-height: 32px;
    }
    .tagpro1,
    .tagpro2 {
      border: none;
      border-radius: 50px;
      height: 26px;
      width: 60px;
      line-height: 26px;
      text-align: center;
      padding: 0;
    }
    .tagpro1 {
      background: rgba(25, 187, 12, 0.15);
    }
    .tagpro2 {
      background: rgba(13, 76, 218, 0.15);
    }
    ::v-deep .ivu-table {
      font-weight: bold;
    }
    ::v-deep .ivu-btn {
      padding: 0 10px;
      font-size: 15px;
      border-radius: 2px;
    }
    .tabpage {
      margin-bottom: 16px;
      /* border-bottom: 1px solid black; */
      width: 100%;
      height: 68px;
      padding: 18px;
      background-color: white;
      .ivu-page {
        float: right;
      }
    }
  }
  ::v-deep .ivu-table th {
    background-color: #f6f7f8;
    color: #a0a8b5;
    height: 48px;

    font-size: 15px;
  }
}
</style>