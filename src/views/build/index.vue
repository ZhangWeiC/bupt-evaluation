<template>
  <div class="single-container">
    <el-card class="single-card">
      <div slot="header" class="card-header">
        <span>各项指标展示</span>
      </div>
      <el-row :gutter="20">
        <el-col v-for="(item, index) in singleArr" :key="index" :span="6">
          <el-card class="single-card-item" shadow="hover">
            <p class="single-card-item-header">
              <span>{{ item.title }}</span>
              <el-tooltip :content="item.content" placement="top">
                <i class="el-icon-info" />
              </el-tooltip>
            </p>
            <div class="single-card-item-value">
              {{ item.value | formatNumber }}{{ item.unit }}
            </div>
            <p class="single-card-item-ava">
              <span>{{ item.subtitle }}：<b>{{ item.average | formatNumber }}{{ item.subunit }}</b></span>
            </p>
          </el-card>
        </el-col>
      </el-row>
    </el-card>
    <el-card class="pro-card">
      <div slot="header" class="card-header">
        <span>xx项目拓扑展示</span>
      </div>
      <div class="pro-card-map">
        地图展示区域
      </div>
      <el-tabs v-model="mapListName" style="margin-top:20px" @tab-click="tabMapChange">
        <el-tab-pane label="节点信息" name="0" />
        <el-tab-pane label="链路信息" name="1" />
        <el-tab-pane label="业务信息" name="2" />
      </el-tabs>
      <el-table
        style="width:100%; margin-top:20px"
        :data="mapTableData"
        stripe
        border
      >
        <el-table-column :label="curMapTableLabel[0]" prop="id" width="80" align="center" />
        <el-table-column :label="curMapTableLabel[1]" prop="name" align="center" />
        <el-table-column :label="curMapTableLabel[2]" prop="coontent" align="center" />
        <el-table-column :label="curMapTableLabel[3]" prop="type" align="center" />
      </el-table>
    </el-card>
    <el-card class="quota-card">
      <el-tabs v-model="activeName" @tab-click="tabChange">
        <el-tab-pane label="项目建设进度" name="0" />
        <el-tab-pane label="项目建设提升" name="1" />
      </el-tabs>
      <div class="quota-card-contain">
        <div class="quota-card-contain-charts">
          <div id="charts" />
        </div>
      </div>
    </el-card>
  </div>
</template>

<script>
// import { getList } from '@/api/table'
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
        { title: '总投资额', content: '该项目总投资额', value: 4560, subtitle: '周均投资额', average: 183, unit: '万', subunit: '万' },
        { title: '当月工程进度', content: '本月该项目工程进度', value: 25, subtitle: '月同比增长', average: 12, unit: '%', subunit: '%' },
        { title: '当周工程进度', content: '本周该项目工程进度', value: 44, subtitle: '日工程进度', average: 1213, unit: '%', subunit: '' },
        { title: '建设匹配度', content: '项目的建设匹配度', value: 78, subtitle: '月同比增长', average: -7, unit: '%', subunit: '%' }
      ],
      mapArr: [
        [
          { id: 1, name: '节点1', coontent: '1,942', type: '普通节点' },
          { id: 2, name: '节点2', coontent: '2,712', type: '普通节点' },
          { id: 3, name: '节点3', coontent: '1,083', type: '普通节点' }
        ],
        [
          { id: 1, name: '链路1', coontent: '1,942', type: '普通链路' },
          { id: 2, name: '链路2', coontent: '2,712', type: '普通链路' },
          { id: 2, name: '链路2', coontent: '2,942', type: '普通链路' },
          { id: 2, name: '链路2', coontent: '3,272', type: '普通链路' },
          { id: 3, name: '链路3', coontent: '1,083', type: '普通链路' }
        ],
        [
          { id: 1, name: '业务1', coontent: '1,942', type: '普通业务' },
          { id: 2, name: '业务2', coontent: '2,712', type: '普通业务' },
          { id: 3, name: '业务3', coontent: '1,083', type: '普通业务' },
          { id: 3, name: '业务3', coontent: '1,083', type: '普通业务' },
          { id: 3, name: '业务3', coontent: '1,083', type: '普通业务' },
          { id: 3, name: '业务3', coontent: '1,083', type: '普通业务' },
          { id: 3, name: '业务3', coontent: '1,083', type: '普通业务' }
        ]
      ],
      activeName: '0',
      mapListName: '0',
      mapTableData: [],
      curMapTableLabel: [],
      mapTableLabel: [
        ['节点ID', '节点名称', '节点容量', '节点类型'],
        ['链路ID', '链路名称', '链路容量', '链路类型'],
        ['业务ID', '业务名称', '业务容量', '业务类型']
      ],
      quotaList: [],
      chart: null,
      quota: [{
        dataAxis: ['正在建设项目数', '完工项目数', '合格项目数', '违约项目数', '不合格项目数', '其他'],
        data: [{
          value: 310,
          name: '正在建设项目数'
        }, {
          value: 123,
          name: '完工项目数'
        }, {
          value: 442,
          name: '合格项目数'
        }, {
          value: 321,
          name: '违约项目数'
        }, {
          value: 149,
          name: '不合格项目数'
        }, {
          value: 210,
          name: '其他'
        }],
        title: '建设进度'
      }, {
        dataAxis: ['正在建设项目数', '完工项目数', '合格项目数', '违约项目数', '不合格项目数', '其他'],
        data: [{
          value: 133,
          name: '正在建设项目数'
        }, {
          value: 334,
          name: '完工项目数'
        }, {
          value: 198,
          name: '合格项目数'
        }, {
          value: 123,
          name: '违约项目数'
        }, {
          value: 125,
          name: '不合格项目数'
        }, {
          value: 220,
          name: '其他'
        }],
        title: '建设提升'
      }],
      option: {
        title: {
          text: '',
          x: 'center',
          y: 'center',
          textStyle: {
            fontWeight: 'normal',
            fontSize: 16
          }
        },
        tooltip: {
          show: true,
          trigger: 'item',
          formatter: '{b}: {c} ({d}%)'
        },
        legend: {
          orient: 'horizontal',
          bottom: '0%',
          data: []
        },
        series: [{
          type: 'pie',
          selectedMode: 'single',
          radius: ['25%', '58%'],
          color: ['#86D560', '#AF89D6', '#59ADF3', '#FF999A', '#FFCC67', '#34C6CD'],

          label: {
            normal: {
              position: 'inner',
              formatter: '{d}%',

              textStyle: {
                color: '#fff',
                fontWeight: 'bold',
                fontSize: 14
              }
            }
          },
          labelLine: {
            normal: {
              show: false
            }
          },
          data: []
        }, {
          type: 'pie',
          radius: ['58%', '83%'],
          itemStyle: {
            normal: {
              color: '#F2F2F2'
            },
            emphasis: {
              color: '#ADADAD'
            }
          },
          label: {
            normal: {
              position: 'inner',
              formatter: '{c}',
              textStyle: {
                color: '#777777',
                fontWeight: 'bold',
                fontSize: 14
              }
            }
          },
          data: []
        }]
      }
    }
  },
  created() {
    this.option.legend.data = this.quota[0].dataAxis
    this.option.series[0].data = this.quota[0].data
    this.option.series[1].data = this.quota[0].data
    this.option.title.text = this.quota[0].title
    this.mapTableData = this.mapArr[0]
    this.curMapTableLabel = this.mapTableLabel[0]
  },
  mounted() {
    this.initCharts()
  },
  methods: {
    initCharts() {
      this.chart = this.$charts.init(document.getElementById('charts'))
      this.chart.setOption(this.option)
    },
    tabChange(e) {
      this.option.legend.data = this.quota[e.name].dataAxis
      this.option.series[0].data = this.quota[e.name].data
      this.option.series[1].data = this.quota[e.name].data
      this.option.title.text = this.quota[e.name].title
      this.chart.setOption(this.option)
    },
    tabMapChange(e) {
      this.mapTableData = this.mapArr[e.name]
      this.curMapTableLabel = this.mapTableLabel[e.name]
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
    .pro-card {
      margin: 15px 20px;
      &-map {
        border: 1px solid black;
        width: 100%;
        height: 300px;
      }
    }
    .quota-card {
      margin: 15px 20px;
      &-contain {
        // border: 1px solid black;
        &-charts {
          width: 800px;
          min-height: 100px;
          // border: 1px solid black;
          margin: 0 auto;
          #charts {
            height: 450px;
            width: 700px;
            margin: 0 auto;
          }
        }
        &-list {
          flex: 1;
          h3 {
            margin-top: 3px;
          }
        }
      }
    }
  }
</style>
