<template>
  <div>
    <!--搜索框         this的指向问题   输入框得手动删除      -->
    <el-form :inline="true" class="demo-form-inline" style="margin-top: 20px;margin-left: 30px;">
      <el-divider content-position="left">库存管理</el-divider>
      <el-form-item label="货物编码:">
        <el-input v-model="goodscode" placeholder="请输入货物编码"></el-input>
      </el-form-item>
      <el-form-item label="货物名称:">
        <el-input v-model="goodsname" placeholder="请输入货物名称"></el-input>
      </el-form-item>
      <el-form-item>
        <el-button type="primary" @click="doSubmit" icon="el-icon-search">查询</el-button>
      </el-form-item>
      <el-form-item>
        <el-button type="info" @click="clearFrom" icon="el-icon-minus">重置</el-button>
      </el-form-item>
      <el-form-item>
        <el-button type="info" @click="show = !show" icon="el-icon-more-outline">更多</el-button>
      </el-form-item><br />
      <div v-if="show">
        <el-form-item label="规格:" style="margin-left: 27px;">
          <el-input v-model="specifications" placeholder="请输入规格"></el-input>
        </el-form-item>
        <br />
      </div>
      <el-button type="primary" @click="exportExcel" icon="el-icon-sort">导出</el-button>
      <!--数据表格-->
      <el-table :data="data1" style=" margin-top:10px;width: 100%;" :border="true" max-height="550" id="rebateSetTable">
        <el-table-column prop="id" label="序号" min-width="20" align="center"></el-table-column>
        <el-table-column prop="goodscode" label="货物编码" min-width="50" align="center"></el-table-column>
        <el-table-column prop="goodsname" label="货物名称" min-width="50" align="center"></el-table-column>
        <el-table-column prop="actualnum" label="数量" min-width="50" align="center"></el-table-column>
        <el-table-column prop="plannedprice" label="计划价格" min-width="40" align="center"></el-table-column>
        <el-table-column prop="specifications" label="规格" min-width="40" align="center"></el-table-column>
        <el-table-column prop="type" label="类型" min-width="40" align="center"></el-table-column>
        <el-table-column prop="measurementunit" label="计量单位" min-width="40" align="center"></el-table-column>
        <el-table-column prop="plannedprice" label="金额" min-width="40" align="center"></el-table-column>
      </el-table>
    </el-form>
  </div>
</template>

<script>
  import axios from 'axios'
  import qs from 'qs'
  import FileSaver from 'file-saver'
  import XLSX from 'xlsx'
  export default {
    name: 'stock',
    data: function() {
      return {
        goodscode: null,
        goodsname: null,
        specifications: null,
        show: false,
        data1: [],
        //对象
        result: []
      }
    },
    methods: {
      exportExcel() {
        let wb = XLSX.utils.table_to_book(document.querySelector('#rebateSetTable'));
        let wbout = XLSX.write(wb, {
          bookType: 'xlsx',
          bookSST: true,
          type: 'array'
        });
        try {
          FileSaver.saveAs(new Blob([wbout], {
            type: 'application/octet-stream'
          }), '库存管理.xlsx');
        } catch (e) {
          if (typeof console !== 'undefined')
            console.log(e, wbout)
        }
        return wbout
      },

      //查询全部的方法
      findAll: function() {
        let url = 'http://localhost/StockItem/findAll';
        axios.post(url, null).then(resp => {
          this.data = resp.data;
          this.result = resp.data;
        }).catch(error => {
          console.log(error);
        });
      },
      //导出
      derive: function() {
        this.$message({
          type: 'info',
          message: '该功能正在开发中'
        });
      },
      //清除表单数据
      clearFrom: function() {
        this.goodscode = null;
        this.measurementunit = null;
        this.specifications = null;
      },
      //多条件查询
      doSubmit: function() {
        this.data1 = this.result;
        if (this.goodscode == null && this.goodsname == null && this.specifications == null) {
          this.findAll();
        }
        if (this.goodscode != null && this.goodscode != "") {
          this.data1 = this.data1.filter(f => f.goodscode.indexOf(this.goodscode) != -1);
        }
        if (this.goodsname != null && this.goodsname != "") {
          this.data1 = this.data1.filter(a => a.goodsname.indexOf(this.goodsname) != -1);
        }
        if (this.specifications != null && this.specifications != "") {
          this.data1 = this.data1.filter(b => b.specifications.indexOf(this.specifications) != -1);
        }
        return this.data1;
        /* this.goodscode=null;
        this.measurementunit=null;
        this.specifications=null;
        this.stocktype=null; */
      }
    },
    //查询全部
    created: function() {
      let url = 'http://localhost/StockItem/findAll';
      axios.post(url, null).then(resp => {
        //console.log(resp.data)
        this.data1 = resp.data;
        this.result = resp.data;
      }).catch(error => {
        console.log(error);
      });
    }
  }
</script>
<style scoped>

</style>
