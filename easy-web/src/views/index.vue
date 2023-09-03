<template>
    <div>
        <el-button type="primary" @click="loadData">新增用户</el-button>
    </div>
    <el-table :data="tableData" style="width: 100%">
        <el-table-column label="用户ID" prop="id"></el-table-column>
        <el-table-column label="用户名" prop="userName"></el-table-column>
        <el-table-column label="手机号" prop="phone"></el-table-column>
        <el-table-column label="出生年月" prop="birthday"></el-table-column>
        <el-table-column label="性别" prop="sex">
            <template #default="scope">
                {{ SEX_MAP[scope.row.sex] }}
            </template>
        </el-table-column>
        <el-table-column label="职位" prop="position">
            <template #default="scope">
                {{ POSITON_MAP[scope.row.position] }}
            </template>
        </el-table-column>
        <el-table-column label="角色" prop="roles">
            <template #default="scope">
                {{ ROLES_MAP[scope.row.position] }}
            </template>
        </el-table-column>
        <el-table-column label="操作">
            <template #default="scope">
                <el-button-group>
                    <el-button 
                    size="small" 
                    type="primary"
                    @click="handleEdit(scope.$index, scope.row)">修改</el-button>
                    <el-button 
                    size="small" 
                    type="primary"
                    @click="handleEdit(scope.$index, scope.row)">修改密码</el-button>
                    <el-button 
                    size="small" type="danger" @click="handleDelete(scope.$index, scope.row)">删除</el-button>
                </el-button-group>
            </template>
        </el-table-column>
    </el-table>
</template>
  
<script setup>
import axios from "axios"
import { ElMessage } from "element-plus"
import { ref, reactive, getCurrentInstance, nextTick } from "vue";
const { proxy } = getCurrentInstance();

const api = {
    loadDataList: "api/list",
};
const SEX_MAP = {
    0: "女",
    1: "男"
};
const POSITON_MAP = {
    0: "程序员",
    1: "测试",
    2: "产品经理"
};
const ROLES_MAP = {
    0: "普通用户",
    1: "组长",
    2: "经理",
    3: "管理员"
};

const tableData = ref([]);

const loadData = async () => {
    const result = await axios.post(api.loadDataList, {});
    const data = result.data;
    console.log(data);
    // if (data.status != "success") {
    //     ElMessage.error("获取数据失败");
    //     return;
    // }
    tableData.value = data;
};

loadData();

</script>
  

<style></style>