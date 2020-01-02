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
            <el-col v-for="(item, index) in recentArr" :key="index" :span="8">
              <el-card class="recent-card-item" shadow="hover">
                <h4 class="recent-card-item-header" @click="transferTo">
                  {{ item.title }}
                </h4>
                <p class="recent-card-item-address">
                  地点：{{ item.address }}
                </p>
                <p class="recent-card-item-descript">
                  项目简述：{{ item.descript }}
                </p>
                <p class="recent-card-item-date" @click="transferTo">
                  {{ item.date }}
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
            <el-table-column prop="operation" label="操作" align="center" width="180">
              <template>
                <el-button
                  size="mini"
                  type="text"
                  @click="transferTo"
                >单项评估</el-button>
                <el-button
                  size="mini"
                  type="text"
                  @click="transferToDouble"
                >综合评估</el-button>
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
          <el-form :inline="true">
            <el-form-item class="quick-card-item">
              <el-button type="text" @click="importClick">一键导入</el-button>
            </el-form-item>
            <el-form-item class="quick-card-item">
              <el-button type="text" @click="searchFormVisible = true">项目查询</el-button>
            </el-form-item>
            <el-form-item class="quick-card-item">
              <el-button type="text" @click="operatVisible = true">操作日志</el-button>
            </el-form-item>
            <el-form-item class="quick-card-item">
              <el-button type="text">操作四</el-button>
            </el-form-item>
            <el-form-item class="quick-card-item">
              <el-button type="text">操作五</el-button>
            </el-form-item>
            <el-form-item class="quick-card-item">
              <el-button type="text">操作六</el-button>
            </el-form-item>
          </el-form>
        </el-card>
        <el-card class="radar-card">
          <div slot="header" class="radar-card-header">
            <span>指标雷达图</span>
          </div>
          <div class="charts-container">
            <div id="charts" />
          </div>
        </el-card>
      </div>
    </div>
    <el-dialog title="项目查询" :visible.sync="searchFormVisible" width="500px" top="200px">
      <el-form>
        <el-form-item label="项目名称：">
          <el-input v-model="searchForm.project" autocomplete="off" />
        </el-form-item>
        <el-form-item label="单位名称：" style="margin-top: 30px">
          <el-input v-model="searchForm.department" autocomplete="off" />
        </el-form-item>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button @click="searchFormVisible = false">取 消</el-button>
        <el-button type="primary" @click="searchFormVisible = false">确 定</el-button>
      </div>
    </el-dialog>
    <el-dialog title="项目查询" :visible.sync="operatVisible" width="500px" top="200px">
      <div>
        <p>18:36 2019/12/30 用户：user1 操作：一键导入 操作结果：成功；</p>
        <p>18:36 2019/12/30 用户：user1 操作：一键导入 操作结果：成功；</p>
        <p>18:36 2019/12/30 用户：user1 操作：一键导入 操作结果：成功；</p>
        <p>18:36 2019/12/30 用户：user1 操作：一键导入 操作结果：成功；</p>
      </div>
      <div slot="footer" class="dialog-footer">
        <!-- <el-button @click="searchFormVisible = false">取 消</el-button> -->
        <el-button type="primary" @click="operatVisible = false">确 定</el-button>
      </div>
    </el-dialog>
  </div>
</template>

<script>
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
        { title: '项目一', address: '教一', descript: '这是需求一这是...', date: '2019-12-27' },
        { title: '项目二', address: '教二', descript: '这是需求二这是...', date: '2019-12-27' },
        { title: '项目三', address: '教三', descript: '这是需求三这是...', date: '2019-12-27' }
      ],
      option: {
        tooltip: {},
        radar: {
          name: {
            textStyle: {
              color: '#fff',
              backgroundColor: '#999',
              borderRadius: 3,
              fontSize: 10,
              padding: [3, 2]
            }
          },
          nameGap: 6,
          indicator: [
            { name: '本月新增项目数', max: 8000 },
            { name: '完工\n项目数', max: 9000 },
            { name: '项目总数', max: 4000 },
            { name: '未完成项目数', max: 6000 },
            { name: '绩效考\n核排名', max: 8000 }
          ]
        },
        series: [
          {
            name: '各指标参数',
            type: 'radar',
            symbol: 'circle',
            symbolSize: 10,
            itemStyle: {
              color: 'rgba(86,199,60, 1)',
              borderColor: 'rgba(86,199,60, 0.3)',
              borderWidth: 10
            },
            lineStyle: {
              normal: {
                color: 'rgba(86,199,60, 1)',
                width: 2
              }
            },
            data: [
              [6560, 8893, 3473, 5273, 6560]
            ]
          }
        ]
      },
      searchFormVisible: false,
      operatVisible: false,
      searchForm: {
        project: '',
        department: ''
      }
    }
  },
  mounted() {
    this.initCharts()
  },
  methods: {
    initCharts() {
      const chart = this.$charts.init(document.getElementById('charts'))
      chart.setOption(this.option)
    },
    importClick() {
      this.$message({
        message: '一键导入成功，项目列表已更新至最新状态',
        type: 'success'
      })
    },
    transferTo() {
      this.$router.push('/single/plan')
    },
    transferToDouble() {
      this.$router.push('/comprehensive/index')
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
		&-left {
			flex: 1;
			overflow: auto;
		}
		&-right {
			width: 350px;
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
    &-item {
      &-header {
        margin: 0;
        cursor: pointer;
      }
      &-header:hover {
        color: #409EFF;
      }
      &-address {
        margin: 10px 0;
        color: #909399;
        font-size: 14px;
      }
      &-descript {
        margin: 10px 0;
        color: #909399;
        font-size: 14px;
      }
      &-date {
        margin: 0;
        text-align: right;
        color: #409EFF;
        font-size: 13px;
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
    &-item {
      margin-left: 5px;
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
    .charts-container {
      width: 100%;
      height: 285px;
      margin-top: 15px;
      margin-left: -10px;
      #charts {
        width: 280px;
        height: 290px;
        margin-left: 8px;
      }
    }
	}
  /deep/ .el-input {
    width: 350px;
  }
}
</style>
