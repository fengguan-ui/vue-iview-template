<template>
  <div class="app-container user-container">
    <!-- 检索区 -->

    <div class="searchArea">
      <Form :model="formItem" :label-width="120" inline>
        <Row>
          <Col span="6">
            <FormItem label="姓名 / 手机号">
              <Input
                v-model="formItem.input"
                placeholder="请输入姓名或手机号进行查询..."
                size="large"
              ></Input>
            </FormItem>
          </Col>
          <Col span="12">
            <FormItem label="角色筛选">
              <CheckboxGroup v-model="border" size="large">
                <Checkbox label="软件试用" border></Checkbox>
                <Checkbox label="装配工" border></Checkbox>
                <Checkbox label="质检员" border></Checkbox>
                <Checkbox label="管理员" border></Checkbox>
              </CheckboxGroup>
            </FormItem>
          </Col>
        </Row>
        <Row>
          <Col span="6">
            <FormItem label="">
              <Button type="primary" size="large">查询</Button>
              <Button type="primary" size="large" style="margin-left: 10px"
                >新增用户</Button
              >
            </FormItem>
          </Col>
        </Row>
      </Form>
    </div>

    <div class="tablecon">
      <Table :columns="columns1" :data="data1">
        <!-- 测量结果 -->
        <template slot-scope="{ row, index }" slot="role">
          <Tag
            :color="
              row.role == '软件试用'
                ? 'green'
                : row.role == '装配工'
                ? 'geekblue'
                : row.role == '质检员'
                ? 'red'
                : 'gold'
            "
            >{{ row.role }}</Tag
          >
        </template>

        <template slot-scope="{ row, index }" slot="act">
          <Button type="primary" style="margin-right: 5px" @click="show(index)"
            >编辑</Button
          >
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
      // 表格
      columns1: [
        {
          title: "公司",
          key: "company",
        },
        {
          title: "姓名",
          key: "name",
        },
        {
          title: "手机号",
          key: "phone",
        },
        {
          title: "角色",
          slot: "role",
        },
        {
          title: "操作",
          slot: "act",
        },
      ],
      data1: [
        {
          company: "华中数控",
          name: "测试员",
          phone: "13624984214",
          role: "软件试用",
        },
        {
          company: "华中数控",
          name: "测试员",
          phone: "13624984214",
          role: "装配工",
        },
        {
          company: "华中数控",
          name: "测试员",
          phone: "13624984214",
          role: "质检员",
        },
        {
          company: "华中数控",
          name: "测试员",
          phone: "13624984214",
          role: "管理员",
        },
      ],
      //表单
      border: ["软件试用"],
      formItem: {
        input: "",
        checkbox: [],
      },
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
.user-container {
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
    ::v-deep .ivu-input {
      width: 260px;
    }
    ::v-deep .ivu-form .ivu-form-item-label {
      font-size: 16px;
      line-height: 1.3;
    }
    ::v-deep .ivu-form-inline .ivu-form-item {
      width: 100%;
      margin-bottom: 10px;
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