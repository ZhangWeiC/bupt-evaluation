<template>
  <div class="project-container">
    <div class="form-contain">
      <el-form :inline="true" class="form-inline">
        <el-form-item label="战 区：" class="pro-form-item">
          <el-select v-model="user" placeholder="活动区域">
            <el-option label="区域一" value="shanghai"></el-option>
            <el-option label="区域二" value="beijing"></el-option>
          </el-select>
        </el-form-item>
        <el-form-item label="军兵种：" class="pro-form-item">
          <el-select v-model="region" placeholder="活动区域">
            <el-option label="区域一" value="shanghai"></el-option>
            <el-option label="区域二" value="beijing"></el-option>
          </el-select>
        </el-form-item>
        <el-form-item label="战略方向：" class="pro-form-item">
          <el-select v-model="region1" placeholder="活动区域">
            <el-option label="区域一" value="shanghai"></el-option>
            <el-option label="区域二" value="beijing"></el-option>
          </el-select>
        </el-form-item>
        <el-form-item class="pro-form-item">
          <el-button type="primary" @click="onSubmit">查询</el-button>
        </el-form-item>
      </el-form>
      
    </div>

    <el-card class="project-card">
      <div slot="header" class="project-card-header">
        <span>项目列表</span>
      </div>
      <el-table
        :data="tableData"
        border
        style="width: 100%"
        max-height="500"
        stripe
      >
        <el-table-column type="index" label="序号" width="80"></el-table-column>
        <el-table-column prop="name" label="项目名称"></el-table-column>
        <el-table-column prop="area" label="战区"></el-table-column>
        <el-table-column prop="type" label="军兵种"></el-table-column>
        <el-table-column prop="direction" label="战略方向"></el-table-column>
        <el-table-column prop="operation" label="操作">
          <template slot-scope="scope">
            <el-button
              size="mini"
              @click="handleEdit(scope.$index, scope.row)">查看拓扑</el-button>
            <el-button
              size="mini"
              type="primary"
              @click="handleDelete(scope.$index, scope.row)">评估</el-button>
          </template>
        </el-table-column>
      </el-table>
      <div class="project-card-pagination">
        <el-pagination
          layout="prev, pager, next"
          :total="1000">
        </el-pagination>
      </div>
    </el-card>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'

export default {
  name: 'Dashboard',
  data() {
    return {
      user: '',
      region: '',
      region1: '',
      tableData: [
        {name: 'xxx', area: '南方战区', type: '海军', direction: 'xxx'},
        {name: 'xxx', area: '南方战区', type: '海军', direction: 'xxx'},
        {name: 'xxx', area: '南方战区', type: '海军', direction: 'xxx'},
        {name: 'xxx', area: '南方战区', type: '海军', direction: 'xxx'},
        {name: 'xxx', area: '南方战区', type: '海军', direction: 'xxx'},
        {name: 'xxx', area: '南方战区', type: '海军', direction: 'xxx'},
        {name: 'xxx', area: '南方战区', type: '海军', direction: 'xxx'}
      ]
    };
  }
}
</script>

<style lang="scss" scoped>
.project-container {
  .form-contain {
    min-height: 80px;
    margin-top: 2px;
    background-color: #fff;
    .form-inline {
      margin-left: 50px;
      .pro-form-item {
        margin-left: 10px;
        margin-top: 15px;
      }
    }
  }
  .project-card {
    margin: 15px 20px;
    &-header {
      span {
        font-size: 18px;
        font-weight: 700;
      }
    }
    &-pagination {
      margin-top: 10px;
      text-align: center;
    }
  }
}
</style>
