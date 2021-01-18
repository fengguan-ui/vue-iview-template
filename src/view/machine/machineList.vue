<template>
  <div class="app-container machineList-container">
    <!-- 检索区 -->

    <div class="searchArea">
      <Form :model="formItem" :label-width="120" inline>
        <Row>
          <Col span="8">
            <FormItem label="装配模板">
              <Select v-model="formItem.select1" size="large">
                <Option
                  v-for="item in template1"
                  :value="item.value"
                  :key="item.value"
                  >{{ item.label }}</Option
                >
              </Select>
            </FormItem>
          </Col>
          <Col span="8">
            <FormItem label="装配步骤">
              <Select v-model="formItem.select2" size="large">
                <Option
                  v-for="item in template2"
                  :value="item.value"
                  :key="item.value"
                  >{{ item.label }}</Option
                >
              </Select>
            </FormItem>
          </Col>
          <Col span="8">
            <FormItem label="检验项">
              <Select v-model="formItem.select3" size="large">
                <Option
                  v-for="item in template3"
                  :value="item.value"
                  :key="item.value"
                  >{{ item.label }}</Option
                >
              </Select>
            </FormItem>
          </Col>
        </Row>
        <Row>
          <Col span="8">
            <FormItem label="日期范围">
              <DatePicker
                type="datetimerange"
                format="yyyy-MM-dd HH:mm"
                placeholder="开始日期 至 结束日期"
                size="large"
              ></DatePicker>
            </FormItem>
          </Col>

          <Col span="8">
            <FormItem label="编号 / 型号">
              <Input
                v-model="formItem.input"
                placeholder="请输入机床编号或产品型号..."
                size="large"
              ></Input>
            </FormItem>
          </Col>
          <Col span="8">
            <FormItem label="关键字搜索">
              <Input
                v-model="formItem.input"
                placeholder="请输入任意关键字进行搜索..."
                size="large"
              ></Input>
            </FormItem>
          </Col>

          <FormItem label="">
            <Button type="primary" size="large">查询</Button>
            <Button type="primary" size="large" style="margin-left: 10px"
              >新建订购卡片</Button
            >
          </FormItem>
        </Row>
      </Form>
    </div>

    <div class="tablecon">
      <Table :columns="columns1" :data="data1">
        <!-- 检测进度 -->

        <template slot-scope="{ row, index }" slot="progress">
          <Tag class="tagpro1" color="green" v-if="row.progress == stepcount">
            {{ row.progress }}
            <font>/</font>
            {{ stepcount }}
          </Tag>

          <Tag class="tagpro2" color="geekblue" v-else>
            {{ row.progress }}
            <font>/</font>
            {{ stepcount }}
          </Tag>
        </template>

        <!-- 检测结果 -->
        <template slot-scope="{ row, index }" slot="result">
          <Tag :color="row.result == '已通过' ? 'green' : 'red'">
            {{ row.result }}
          </Tag>
        </template>

        <template slot-scope="{ row, index }" slot="act">
          <Button type="primary" style="margin-right: 5px">检测详情</Button>
          <Button type="primary" style="margin-right: 5px" @click="show(index)"
            >编辑</Button
          >
          <Button style="margin-right: 5px">查看</Button>
          <Button type="error" @click="remove(index)">删除</Button>
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
      // 装配模板下拉框
      template1: [
        { value: "1", label: "高速五轴" },
        { value: "2", label: "高速五轴22" },
      ],
      template2: [
        { value: "1", label: "步骤11" },
        { value: "2", label: "步骤9283892" },
      ],
      template3: [
        { value: "1", label: "检验项11" },
        { value: "2", label: "检验项134450300" },
      ],
      formItem: {
        select1: "",
        select2: "",
        select3: "",
        input: "",
        datetimerange: "",
      },

      // 步骤总数
      stepcount: 40,

      // 表格
      columns1: [
        {
          title: "机床编号",
          key: "No",
        },
        {
          title: "产品型号",
          key: "model",
        },
        {
          title: "产品类型",
          key: "type",
        },
        {
          title: "订货日期",
          key: "otime",
        },
        {
          title: "交货日期",
          key: "ctime",
        },
        {
          title: "检测进度",
          slot: "progress",
          width: 100,
        },
        {
          title: "检测结果",
          slot: "result",
          width: 120,
        },
        {
          title: "操作",
          slot: "act",
          width: 300,
        },
      ],
      data1: [
        {
          No: "J8230",
          model: "Aaron",
          type: "Aoki",
          otime: "2020-12-1 10:26:49",
          ctime: "2020-12-12 10:26:49",
          progress: "40",
          result: "已通过",
        },
        {
          No: "J8230",
          model: "Aaron",
          type: "Aoki",
          otime: "2020-12-1 10:26:49",
          ctime: "2020-12-12 10:26:49",
          progress: "16",
          result: "未通过",
        },
      ],
    };
  },
  methods: {
    show(index) {
      this.$Modal.info({
        title: "User Info",
        content: `Name：${this.data1[index].name}`,
      });
    },
    remove(index) {
      this.data1.splice(index, 1);
    },
  },
};
</script>
<style lang="scss" scoped>
.machineList-container {
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