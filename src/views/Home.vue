<template>
  <div class="home">
    <el-row>
      <el-col :span="12">
        <p style="margin-top:20px;">Table Expand Example</p>
        <el-table ref="table" size="small" :data="tableData" stripe border style="width: 800px;margin:20px auto;">
          <el-table-column label="商品 ID" prop="id.value"></el-table-column>
          <el-table-column label="商品名称" prop="name.value"></el-table-column>
          <el-table-column label="描述" prop="desc.value"></el-table-column>
          <el-table-column label="操作" width="100" align="center">
            <template slot-scope="scope">
              <el-button type="text" @click="toogleExpand(scope.row)">{{scope.row.expansion ? '收起' : '查看详情'}}</el-button>
            </template>
          </el-table-column>
          <el-table-column type="expand" width="1">
            <template slot-scope="props">
              <el-form label-position="left" inline class="demo-table-expand">
                <el-form-item :label="item.key" v-for="(item, index) in props.row" :key="item.value" :index="index">
                  <el-popover v-if="item.key != '商品 ID'" placement="top" width="240" :value="item.visible">
                    <el-input type="textarea" :autosize="{ minRows: 2, maxRows: 4}" placeholder="请输入内容" v-model="popoverInput"></el-input>
                    <div style="text-align: right; margin: 10px 0 0">
                      <el-button size="mini" type="text" @click="clickDom()">取消</el-button>
                      <el-button type="primary" size="mini" @click="confirmChange(item)">确定</el-button>
                    </div>
                    <span style="cursor:pointer;" slot="reference" @click="showPopover(item)">{{ item.value }}</span>
                  </el-popover>
                  <span v-else>{{ item.value }}</span>
                </el-form-item>
              </el-form>
            </template>
          </el-table-column>
        </el-table>
      </el-col>
      <el-col :span="12">
        <p style="margin-top:20px;">Data Contrast</p>
        <p v-for="(item, index) in tableData" :key="item.id.value" :index="index">
          {{item.id.value}}
          {{item.name.value}}
          {{item.shop.value}}
          {{item.shopId.value}}
          {{item.category.value}}
          {{item.address.value}}
          {{item.desc.value}}
        </p>
      </el-col>
    </el-row>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'home',
  data() {
    return {
      popoverInput: '',
      tableData: [{
        id: {
          key: '商品 ID',
          value: '12987122',
          visible: false,
        },
        name: {
          key: '商品名称',
          value: '好滋好味鸡蛋仔',
          visible: false,
        },
        shop: {
          key: '所属店铺',
          value: '王小虎夫妻店',
          visible: false,
        },
        shopId: {
          key: '店铺 ID',
          value: '10333',
          visible: false,
        },
        category: {
          key: '商品分类',
          value: '江浙小吃、小吃零食',
          visible: false,
        },
        address: {
          key: '店铺地址',
          value: '上海市普陀区真北路',
          visible: false,
        },
        desc: {
          key: '商品描述',
          value: '荷兰优质淡奶，奶香浓而不腻',
          visible: false,
        },
      }, {
        id: {
          key: '商品 ID',
          value: '12987123',
          visible: false,
        },
        name: {
          key: '商品名称',
          value: '好滋好味鸡蛋仔',
          visible: false,
        },
        shop: {
          key: '所属店铺',
          value: '王小虎夫妻店',
          visible: false,
        },
        shopId: {
          key: '店铺 ID',
          value: '10333',
          visible: false,
        },
        category: {
          key: '商品分类',
          value: '江浙小吃、小吃零食',
          visible: false,
        },
        address: {
          key: '店铺地址',
          value: '上海市普陀区真北路',
          visible: false,
        },
        desc: {
          key: '商品描述',
          value: '荷兰优质淡奶，奶香浓而不腻',
          visible: false,
        },
      }, {
        id: {
          key: '商品 ID',
          value: '12987124',
          visible: false,
        },
        name: {
          key: '商品名称',
          value: '好滋好味鸡蛋仔',
          visible: false,
        },
        shop: {
          key: '所属店铺',
          value: '王小虎夫妻店',
          visible: false,
        },
        shopId: {
          key: '店铺 ID',
          value: '10333',
          visible: false,
        },
        category: {
          key: '商品分类',
          value: '江浙小吃、小吃零食',
          visible: false,
        },
        address: {
          key: '店铺地址',
          value: '上海市普陀区真北路',
          visible: false,
        },
        desc: {
          key: '商品描述',
          value: '荷兰优质淡奶，奶香浓而不腻',
          visible: false,
        },
      }, {
        id: {
          key: '商品 ID',
          value: '12987125',
          visible: false,
        },
        name: {
          key: '商品名称',
          value: '好滋好味鸡蛋仔',
          visible: false,
        },
        shop: {
          key: '所属店铺',
          value: '王小虎夫妻店',
          visible: false,
        },
        shopId: {
          key: '店铺 ID',
          value: '10333',
          visible: false,
        },
        category: {
          key: '商品分类',
          value: '江浙小吃、小吃零食',
          visible: false,
        },
        address: {
          key: '店铺地址',
          value: '上海市普陀区真北路',
          visible: false,
        },
        desc: {
          key: '商品描述',
          value: '荷兰优质淡奶，奶香浓而不腻',
          visible: false,
        },
      },
      ]
    }
  },
  created() {
    let tableData = this.tableData
    tableData.map(item => {
      item.expansion = false
    })
  },
  methods: {
    toogleExpand(row) {
      let $table = this.$refs.table;
      this.tableData.map(item => {
        if (row.id != item.id) {
          $table.toggleRowExpansion(item, false)
          item.expansion = false
        } else {
          item.expansion = !item.expansion
        }
      })
      $table.toggleRowExpansion(row)
    },
    clickDom() {
      document.querySelector("#app").click();
    },
    showPopover(item) {
      console.log(item)
      this.popoverInput = item.value
    },
    confirmChange(item) {
      console.log(item)
      item.value = this.popoverInput
      this.clickDom()
    }
  }
}
</script>

<style>
.demo-table-expand {
  font-size: 0;
}
.demo-table-expand label {
  width: 90px;
  color: #99a9bf;
}
.demo-table-expand .el-form-item {
  margin-right: 0;
  margin-bottom: 0;
  width: 50%;
}
</style>