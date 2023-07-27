<script setup>
import { ref } from "vue";

// 数据
let queryInput = $ref("")
let tableData = $ref([
  {
    id:"1",
    name: 'Tom',
    email:"163@qq.com",
    phone:"18056789863",
    state: 'California',
    address: 'No. 189, Grove St, Los Angeles',
  },
  {
    id:"2",
    name: 'Tom',
    email:"163@qq.com",
    phone:"18056789863",
    state: 'California',
    address: 'No. 189, Grove St, Los Angeles',
  },
  {
    id:"3",
    name: 'Tom',
    email:"163@qq.com",
    phone:"18056789863",
    state: 'California',
    address: 'No. 189, Grove St, Los Angeles',
  },
  {
    id:"4",
    name: 'Tom',
    email:"163@qq.com",
    phone:"18056789863",
    state: 'California',
    address: 'No. 189, Grove St, Los Angeles',
  },
 ])
let multipleSelection = $ref([])
let dialogFormVisible = $ref(false)
let tableForm = ref({
  name:"wangergou",
  email:"107258@qq.com",
  phone:"1560015600",
  state:"在职",
  address:"上海"
})
let dialogType = $ref('add')


// 方法
// 注册事件
const handleRowDel = ({id}) =>{
  console.log(id)
}
const handleSelectionChange = (val) => {
  multipleSelection = val
  console.log(val)
}
const handleAdd = ()=>{       //增加
  dialogFormVisible = true
  tableForm.value = {}
  
}
const dialogConfirm = () =>{    //确认新增
  dialogFormVisible = false
  // 1.拿到数据

  // 2.添加数据到table
  tableData.push({
    id:(tableData.length+1).toString(),
    ...tableForm.value
  })
  console.log(tableData)

}

//开启$ref 不能使用watch监听 
</script>

<template>
  <!-- 创建根元素，防止变量冲突 -->
  <div class="table-box">
    <!-- 标题 -->
    <div class="title">
      <h2>最简单的CRUD Demo</h2>
    </div>
    <!-- query -->
    <div class="query-box">
      <el-input class="query-input" v-model="queryInput" placeholder="请输入姓名搜索" />
      <el-button type="primary" @click="handleAdd">增加</el-button>
    </div>
     <!-- table -->
    <el-table ref="multipleTableRef"
      :data="tableData"
      style="width: 100%"
      @selection-change="handleSelectionChange" border>
      <el-table-column type="selection" width="55" />
      <el-table-column prop="name" label="姓名" width="120" />
      <el-table-column prop="email" label="邮件" width="120" />
      <el-table-column prop="phone" label="电话" width="120" />
      <el-table-column prop="state" label="状态" width="120" />
      <el-table-column prop="address" label="地址" width="400" />
  
      <el-table-column fixed="right" label="操作" width="120">
        <template #default="scoped">
          <el-button link type="primary" size="small" @click="handleRowDel(scoped.row)" style="color:#F56C6C">
            删除
          </el-button>
          <el-button link type="primary" size="small">编辑</el-button>
        </template>
      </el-table-column>
    </el-table>
    <!-- dialog -->
    <el-dialog v-model="dialogFormVisible" :title="dialogType === 'add' ? '新增':'编辑'">
    <el-form :model="tableForm">
      <el-form-item label="姓名" :label-width="80">
        <el-input v-model="tableForm.name" autocomplete="off" />
      </el-form-item>
      <el-form-item label="邮件" :label-width="80">
        <el-input v-model="tableForm.email" autocomplete="off" />
      </el-form-item>
      <el-form-item label="手机" :label-width="80">
        <el-input v-model="tableForm.phone" autocomplete="off" />
      </el-form-item>
      <el-form-item label="状态" :label-width="80">
        <el-input v-model="tableForm.state" autocomplete="off" />
      </el-form-item>
      <el-form-item label="地址" :label-width="80">
        <el-input v-model="tableForm.address" autocomplete="off" />
      </el-form-item>
    </el-form>
    <template #footer>
      <span class="dialog-footer">
        <!-- <el-button @click="dialogFormVisible = false">Cancel</el-button> -->
        <el-button type="primary" @click="dialogConfirm">
          确认
        </el-button>
      </span>
    </template>
  </el-dialog>
   </div>


</template>


<style scoped>
.table-box{
  margin: 200px auto;
  width: 800px;
  /* position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%,-50%); */
}
.title{
  text-align: center;
}
.query-box{
  display: flex;
  justify-content: space-between;
  margin-top: 20px;
  margin-bottom: 20px;
}
.query-input{
  width: 200px;
}

</style>
