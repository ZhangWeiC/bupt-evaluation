<template>
  <div class="single-container">
    <el-card class="single-card">
      <div slot="header" class="card-header">
        <span>单项指标展示</span>
      </div>
      <el-row :gutter="20">
        <el-col :span="6" v-for="(item, index) in singleArr" :key="index">
          <el-card class="single-card-item" shadow="hover">
            <p class="single-card-item-header">
              <span>{{item.title}}</span>
              <el-tooltip :content='item.content' placement="top">
                <i class="el-icon-info"></i>
              </el-tooltip>
            </p>
            <div class="single-card-item-value">
              {{item.value | formatNumber}}
            </div>
            <p class="single-card-item-ava">
              <span>平均值：<b>{{item.average | formatNumber}}</b></span>
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
        <div id="charts"></div>
      </div>
    </el-card>
  </div>
</template>

<script>
import { getList } from '@/api/table'
import numeral from 'numeral'

export default {
  filters: {
    formatNumber(value) {
      return numeral(value).format('0,0')
    }
  },
  data() {
    return {
      singleArr: [
        {title: '拓扑平均度', content: '拓扑平均度的解释', value: 6560, average: 5320},
        {title: '节点平均度', content: '节点平均度的解释', value: 8893, average: 7392},
        {title: '平均路径长度', content: '平均路径长度的解释', value: 3473, average: 3966},
        {title: '拓扑联通度', content: '拓扑联通度的解释', value: 5273, average: 5867}
      ],
      reData: [6560, 8893, 3473, 5273],
      thData: [5320, 7392, 3966, 5867],
      option: {
        title: {
          text: "全指标对比展示图",
          left: "center"
        },
        tooltip : {
            trigger: 'axis',
            axisPointer : {
                type : 'shadow'
            },
            formatter: function (params) {
              return `${params[0].name}
                <br>平均值：${params[0].value} 
                <br>实际值：${-params[1].value}`;
            }
        },
        legend: {
            data:['平均值', '实际值'],
            left: "right",
        },
        grid: {
          left: '3%',
          right: '4%',
          bottom: '3%',
          containLabel: true
        },
        xAxis: [
          {
            type : 'value',
            show: true,
            splitLine: {
              show: true,
              lineStyle: {
                color: '#1F2022',
                width: 1,
                type: 'solid',
              },
            },
            axisLabel: {
              show: false,
            }
          }
        ],
        yAxis : [
          {
            type : 'category',
            axisTick : {show: false},
            data : ['拓扑联通度','平均路径长度','节点平均度','拓扑平均度']
          }
        ],
        series : [
          {
            name:'实际值',
            type:'bar',
            stack: '总量',
            label: {
                normal: {
                    show: true
                }
            },
            itemStyle: {
              color: '#5e94dd'
            },
            data:[6560, 8893, 3473, 5273]
          },
          {
            name:'平均值',
            type:'bar',
            stack: '总量',
            label: {
                normal: {
                    show: true,
                    formatter: function(params){return -params.value}
                }
            },
            itemStyle: {
              color: '#49b5bd'
            },
            data:[-5320, -7392, -3966, -5867]
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
      let chart = this.$charts.init(document.getElementById('charts'));
      chart.setOption(this.option);
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
  .single-container {
    .single-card {
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
        height: 350px;
        // border: 1px solid black;
        margin: 0 auto;
        margin-top: 30px;
      }
      #charts {
        // border: 1px solid black;
        margin: 0 auto;
        width: 700px;
        height: 300px;
      }
    }
  }
</style>
