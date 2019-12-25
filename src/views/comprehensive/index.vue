<template>
  <div class="compre-container">
    <el-card class="compre-card">
      <div slot="header" class="card-header">
        <span>综合评估</span>
      </div>
      <el-row :gutter="20">
        <el-col v-for="(item, index) in singleArr" :key="index" :span="6">
          <el-card class="compre-card-item" shadow="hover">
            <p class="compre-card-item-header">
              <span>{{ item.title }}</span>
              <el-tooltip :content="item.content" placement="top">
                <i class="el-icon-info" />
              </el-tooltip>
            </p>
            <div class="compre-card-item-value">
              {{ item.value | formatNumber }}
            </div>
            <p class="compre-card-item-ava">
              <span>平均值：<b>{{ item.average | formatNumber }}</b></span>
            </p>
          </el-card>
        </el-col>
      </el-row>
      <el-row :gutter="20" style="margin-top: 15px">
        <el-col v-for="(item, index) in singleArr" :key="index" :span="6">
          <el-card class="compre-card-item" shadow="hover">
            <p class="compre-card-item-header">
              <span>{{ item.title }}</span>
              <el-tooltip :content="item.content" placement="top">
                <i class="el-icon-info" />
              </el-tooltip>
            </p>
            <div class="compre-card-item-value">
              {{ item.value | formatNumber }}
            </div>
            <p class="compre-card-item-ava">
              <span>平均值：<b>{{ item.average | formatNumber }}</b></span>
            </p>
          </el-card>
        </el-col>
      </el-row>
      <el-row :gutter="20" style="margin-top: 15px">
        <el-col v-for="(item, index) in singleArr1" :key="index" :span="6">
          <el-card class="compre-card-item" shadow="hover">
            <p class="compre-card-item-header">
              <span>{{ item.title }}</span>
              <el-tooltip :content="item.content" placement="top">
                <i class="el-icon-info" />
              </el-tooltip>
            </p>
            <div class="compre-card-item-value">
              {{ item.value | formatNumber }}
            </div>
            <p class="compre-card-item-ava">
              <span>平均值：<b>{{ item.average | formatNumber }}</b></span>
            </p>
          </el-card>
        </el-col>
      </el-row>
    </el-card>
    <el-card class="all-card">
      <div slot="header" class="card-header">
        <span>全指标展示</span>
      </div>
      <div class="charts-container">
        <div id="charts" />
      </div>
    </el-card>
  </div>
</template>

<script>
export default {
  data() {
    return {
      singleArr: [
        { title: '拓扑平均度', content: '拓扑平均度的解释', value: 6560, average: 5320 },
        { title: '节点平均度', content: '节点平均度的解释', value: 8893, average: 7392 },
        { title: '平均路径长度', content: '平均路径长度的解释', value: 3473, average: 3966 },
        { title: '拓扑联通度', content: '拓扑联通度的解释', value: 5273, average: 5867 }
      ],
      singleArr1: [
        { title: '拓扑平均度', content: '拓扑平均度的解释', value: 6560, average: 5320 },
        { title: '节点平均度', content: '节点平均度的解释', value: 8893, average: 7392 }
      ],
      option: {
        title: {
          text: '指标雷达图'
        },
        tooltip: {},
        legend: {
          data: ['平均值', '实际值'],
          left: 'right'
        },
        radar: {
          name: {
            textStyle: {
              color: '#fff',
              backgroundColor: '#999',
              borderRadius: 3,
              padding: [3, 5]
            }
          },
          indicator: [
            { name: '指标1', max: 8000 },
            { name: '指标2', max: 9000 },
            { name: '指标3', max: 4000 },
            { name: '指标4', max: 6000 },
            { name: '指标5', max: 8000 },
            { name: '指标6', max: 9000 },
            { name: '指标7', max: 4000 },
            { name: '指标8', max: 6000 },
            { name: '指标9', max: 8000 },
            { name: '指标10', max: 9000 }
          ]
        },
        series: [
          {
            name: '实际值',
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
              [6560, 8893, 3473, 5273, 6560, 8893, 3473, 5273, 6560, 8893]
            ]
          },
          {
            name: '平均值',
            type: 'radar',
            symbol: 'circle',
            symbolSize: 10,
            itemStyle: {
              color: 'rgba(0,183,238, 1)',
              borderColor: 'rgba(0,183,238, 0.4)',
              borderWidth: 10
            },
            lineStyle: {
              normal: {
                color: 'rgba(0,183,238, 1)',
                width: 2
              }
            },
            data: [
              [5320, 7392, 3966, 5867, 5320, 7392, 3966, 5867, 5320, 7392]
            ]
          }
        ]
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
    }
  }
}
</script>

<style lang="scss" scoped>
  .card-header {
    span {
      font-size: 18px;
      font-weight: 700;
    }
  }
  .compre-container {
    .compre-card {
      max-height: 380px;
      overflow: auto;
      margin: 15px 20px;
      &-item {
        &-value {
          font-size: 28px;
          font-weight: 400;
          margin: 0;
          color: #409EFF;
          padding-bottom: 10px;
          border-bottom: 1px solid #DCDFE6;
        }
        &-header {
          font-size: 13px;
          color: #606266;
          margin: 0;
          margin-bottom: 10px;
          i {
            float: right;
          }
        }
        &-ava {
          margin: 0;
          font-size: 15px;
          overflow: hidden;
          margin-top: 10px;
          span {
            float: right;
            b {
              font-weight: 500;
              color: #409EFF;
            }
          }
        }
        /deep/ .el-icon-info:hover {
          cursor: pointer;
        }
      }
    }
    .all-card {
      margin: 15px 20px;
      .charts-container{
        height: 500px;
        // border: 1px solid black;
        margin: 0 auto;
        // margin-top: 30px;
      }
      #charts {
        // border: 1px solid black;
        margin: 0 auto;
        width: 700px;
        height: 510px;
      }
    }
  }
</style>

