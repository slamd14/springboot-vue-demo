<template>
  <div style="padding: 10px">
<!--    功能区域-->
    <div style="margin: 10px 0">
      <el-button type="primary" @click="add">新增</el-button>
      <el-button type="primary">导入</el-button>
      <el-button type="primary">导出</el-button>
    </div>
<!--    搜索区域-->
    <div style="margin: 10px 0">
      <el-input v-model="search" placeholder="请输入关键字" style="width: 15%"/>
      <el-button type="primary" style="margin-left: 5px">查询</el-button>
    </div>
<!--    表格-->
    <el-table :data="tableData" border stripe style="width: auto">
      <el-table-column prop="id" label="ID" sortable/>
      <el-table-column prop="username" label="用户名"/>
      <el-table-column prop="nickname" label="昵称"/>
      <el-table-column prop="age" label="年龄"/>
      <el-table-column prop="sex" label="性别"/>
      <el-table-column prop="address" label="地址"/>
      <el-table-column fixed="right" label="操作" width="120">
        <template #default>
          <el-button link type="primary" size="small" @click="handleEdit">编辑</el-button>
          <el-popconfirm title="确认删除吗?">
            <template #reference>
              <el-button link type="primary" size="small">删除</el-button>
            </template>
          </el-popconfirm>
        </template>
      </el-table-column>
    </el-table>
<!--    分页-->
    <div style="margin: 10px 0">
      <div class="demo-pagination-block">
        <div class="demonstration"></div>
        <el-pagination
            current-page="currentPage"
            :page-size="100"
            :page-sizes="[5, 10, 15, 20]"
            layout="total, sizes, prev, pager, next, jumper"
            :total="total"
            @size-change="handleSizeChange"
            @current-change="handleCurrentChange"
        />
      </div>
    </div>

<!--    添加新用户弹窗-->
    <el-dialog
        v-model="dialogVisible"
        title="Tips"
        width="30%"
    >
      <template #footer>
      <span class="dialog-footer">
        <el-button @click="dialogVisible = false">取消</el-button>
        <el-button type="primary" @click="onSubmit">
          确认
        </el-button>
      </span>
      </template>

      <!--    添加新用户表单-->
      <el-form :model="form" label-width="120px">
        <el-form-item label="ID">
          <el-input v-model="form.id" style="height: 120%; width: 30%"/>
        </el-form-item>
        <el-form-item label="用户名">
          <el-input v-model="form.username" style="height: 120%; width: 80%"/>
        </el-form-item>
        <el-form-item label="昵称">
          <el-input v-model="form.nickname" style="height: 120%; width: 80%"/>
        </el-form-item>
        <el-form-item label="年龄">
          <el-input v-model="form.age" style="height: 120%; width: 30%"/>
        </el-form-item>
        <el-form-item label="性别">
          <el-radio-group v-model="form.sex">
            <el-radio label="男" />
            <el-radio label="女" />
          </el-radio-group>
        </el-form-item>
        <el-form-item label="住址">
          <el-input v-model="form.address" type="textarea" />
        </el-form-item>
      </el-form>

    </el-dialog>


  </div>
</template>

<script>

import request from "@/utils/request";

export default {
  name: 'HomeView',
  components: {

  },
  data(){
    return{
      form: {},
      dialogVisible: false,
      search: '',
      currentPage: 1,
      total: 100,
      tableData: [
        {
          date: '2016-05-03',
          name: 'Tom',
          address: 'No. 189, Grove St, Los Angeles',
        },
        {
          date: '2016-05-02',
          name: 'Tom',
          address: 'No. 189, Grove St, Los Angeles',
        },
        {
          date: '2016-05-04',
          name: 'Tom',
          address: 'No. 189, Grove St, Los Angeles',
        },
        {
          date: '2016-05-01',
          name: 'Tom',
          address: 'No. 189, Grove St, Los Angeles',
        },
      ]
    }
  },
  methods: {
    handleEdit() {

    },
    handleSizeChange() {

    },
    handleCurrentChange() {

    },
    add() {
        this.dialogVisible = true;
        this.form = {}; //清空表单中所有属性
    },
    onSubmit(){
        this.dialogVisible = false;
        //提交表单:
        request.post("/api/user", this.form).then(res => {
          console.log(res)
        })
    }
  }
}
</script>
