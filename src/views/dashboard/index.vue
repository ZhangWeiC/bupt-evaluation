<template>
  <div class="project-container">
    <el-card class="header-card">
      <el-row>
        <el-col :span="14">
          <div class="left-header">
            <div class="left-header-img" />
            <div class="left-header-descipt">
              <h3>
                能打胜战，作风优良
              </h3>
              <p>
                <span>XX作战中心坐席1</span>
                <span>xxxx-平台数据技术部门-基础平台部</span>
              </p>
            </div>
          </div>
        </el-col>
        <el-col :span="10">
          <el-row class="right-header">
            <el-col :span="8" style="border-right: 1px solid #DCDFE6">
              <p class="right-header-item">
                项目总数
              </p>
              <h3>56</h3>
            </el-col>
            <el-col :span="8" style="border-right: 1px solid #DCDFE6">
              <p class="right-header-item">
                统计指标1
              </p>
              <h3>8,921</h3>
            </el-col>
            <el-col :span="8">
              <p class="right-header-item">
                统计指标2
              </p>
              <h3>2,223</h3>
            </el-col>
          </el-row>
        </el-col>
      </el-row>
    </el-card>
    <div class="main-contain">
      <div class="main-contain-left">
        <el-card class="recent-card">
          <div slot="header" class="recent-card-header">
            <span>最近浏览的项目</span>
          </div>
          <el-row :gutter="20">
            <el-col v-for="(item, index) in recentArr" :key="index" :span="6">
              <el-card class="recent-card-item" shadow="hover">
                <p class="recent-card-item-header">
                  <span>{{ item.title }}</span>
                </p>
              </el-card>
            </el-col>
          </el-row>
        </el-card>
        <el-card class="project-card">
          <div slot="header" class="project-card-header">
            <span>全部项目</span>
          </div>
          <el-table :data="tableData" border style="width: 100%" max-height="250" stripe>
            <el-table-column type="index" label="序号" width="80" align="center" />
            <el-table-column prop="name" label="项目名称" align="center" />
            <el-table-column prop="area" label="战区" align="center" />
            <el-table-column prop="type" label="军兵种" align="center" />
            <el-table-column prop="direction" label="战略方向" align="center" />
            <el-table-column prop="operation" label="操作" align="center">
              <template slot-scope="scope">
                <el-button
                  size="mini"
                  type="primary"
                  @click="handleDelete(scope.$index, scope.row)"
                >查看详情</el-button>
              </template>
            </el-table-column>
          </el-table>
          <div class="project-card-pagination">
            <el-pagination layout="prev, pager, next" :total="1000" />
          </div>
        </el-card>
      </div>
      <div class="main-contain-right">
        <el-card class="quick-card">
          <div slot="header" class="quick-card-header">
            <span>快速开始</span>
          </div>
        </el-card>
        <el-card class="radar-card">
          <div slot="header" class="radar-card-header">
            <span>指标雷达图</span>
          </div>
        </el-card>
      </div>
    </div>

  </div>
</template>

<script>
// import { mapGetters } from 'vuex'

export default {
  name: 'Dashboard',
  data() {
    return {
      user: '',
      region: '',
      region1: '',
      tableData: [
        { name: 'xxx', area: '南方战区', type: '海军', direction: 'xxx' },
        { name: 'xxx', area: '南方战区', type: '海军', direction: 'xxx' },
        { name: 'xxx', area: '南方战区', type: '海军', direction: 'xxx' },
        { name: 'xxx', area: '南方战区', type: '海军', direction: 'xxx' },
        { name: 'xxx', area: '南方战区', type: '海军', direction: 'xxx' },
        { name: 'xxx', area: '南方战区', type: '海军', direction: 'xxx' },
        { name: 'xxx', area: '南方战区', type: '海军', direction: 'xxx' }
      ],
      recentArr: [
        { title: '需求一' },
        { title: '需求一' },
        { title: '需求一' },
        { title: '需求一' }
      ]
    }
  }
}
</script>

<style lang="scss" scoped>
.project-container {
	.header-card {
			margin: 15px 20px;
			height: 110px;
	}
	.left-header {
		display: flex;
		width: 100%;
	}
	.left-header-img {
		width: 85px;
		height: 70px;
		background: url('./static/img/WechatIMG101.jpeg');
		background-size: cover;
	}
	.left-header-descipt {
		flex: 1;
		h3 {
			margin: 10px;
		}
		p {
			margin-left: 10px;
			margin-top: 15px;
			font-size: 11px;
			color: #909399;
			span:nth-child(1) {
				padding-right: 10px;
			}
			span:nth-child(2) {
				border-left: 1px solid #909399;
				padding-left: 10px;
			}
		}
	}
	.right-header {
		.right-header-item {
			font-size: 14px;
			color: #909399;
			margin-bottom: 10px;
			text-align: center;
		}
		h3 {
			margin: 10px 0;
			font-size: 22px;
			font-weight: 500;
			text-align: center;
		}
	}
	.main-contain {
		width: 100%;
		display: flex;
		border: 1px solid black;
		// height: 100px;
		&-left {
			flex: 1;
			overflow: auto;
		}
		&-right {
			width: 350px;
			border: 1px solid black;
		}
	}
	.project-card {
		margin: 15px 20px;
		&-header {
			span {
				font-size: 16px;
				font-weight: 700;
			}
		}
		&-pagination {
			margin-top: 10px;
			text-align: center;
		}
	}
	.recent-card {
		margin: 15px 20px;
		margin-bottom: 30px;
		&-header {
			span {
				font-size: 16px;
				font-weight: 700;
			}
		}
  }
	.quick-card {
		margin: 15px 20px;
		margin-bottom: 30px;
		&-header {
			span {
				font-size: 16px;
				font-weight: 700;
			}
		}
	}
	.radar-card {
		margin: 15px 20px;
		margin-bottom: 30px;
		&-header {
			span {
				font-size: 16px;
				font-weight: 700;
			}
		}
	}
}
</style>
