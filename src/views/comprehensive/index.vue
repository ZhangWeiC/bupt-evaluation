<template>
  <div class="compre-container">
    <el-card class="compre-card">
      <div slot="header" class="card-header">
        <span>层次分析法</span>
      </div>
      <el-steps :active="step">
        <el-step title="步骤 1" description="构建层次分析模型" />
        <el-step title="步骤 2" description="填写对比矩阵" />
        <el-step title="步骤 3" description="可视化结果展示" />
      </el-steps>
    </el-card>
    <el-card class="step-card">
      <div v-show="step === 1" class="step-card-one">
        <el-form>
          <el-form-item label="目标层：" style="margin-bottom: 30px">
            <el-input v-model="formConfig.target" placeholder="请输入内容" />
          </el-form-item>
          <el-form-item label="准则层：" style="margin-bottom: 30px">
            <el-checkbox-group v-model="formConfig.checklist">
              <el-checkbox label="准则层1" />
              <el-checkbox label="准则层2" />
              <el-checkbox label="准则层3" />
              <el-checkbox label="准则层4" />
            </el-checkbox-group>
          </el-form-item>
          <el-form-item style="margin-bottom: 40px">
            <el-form inline>
              <el-form-item label="准则层1：">
                <el-select v-model="formConfig.selectOne" multiple placeholder="请选择" :disabled="testCheck('准则层1')">
                  <el-option
                    v-for="item in options"
                    :key="item.value"
                    :label="item.label"
                    :value="item.value"
                  />
                </el-select>
              </el-form-item>
              <el-form-item label="准则层2：" style="margin-left: 30px">
                <el-select v-model="formConfig.selectTwo" multiple placeholder="请选择" :disabled="testCheck('准则层2')">
                  <el-option
                    v-for="item in options"
                    :key="item.value"
                    :label="item.label"
                    :value="item.value"
                  />
                </el-select>
              </el-form-item>
            </el-form>
          </el-form-item>
          <el-form-item style="margin-bottom: 30px">
            <el-form inline>
              <el-form-item label="准则层3：">
                <el-select v-model="formConfig.selectThree" multiple placeholder="请选择" :disabled="testCheck('准则层3')">
                  <el-option
                    v-for="item in options"
                    :key="item.value"
                    :label="item.label"
                    :value="item.value"
                  />
                </el-select>
              </el-form-item>
              <el-form-item label="准则层4：" style="margin-left: 30px">
                <el-select v-model="formConfig.selectFour" multiple placeholder="请选择" :disabled="testCheck('准则层4')">
                  <el-option
                    v-for="item in options"
                    :key="item.value"
                    :label="item.label"
                    :value="item.value"
                  />
                </el-select>
              </el-form-item>
            </el-form>
          </el-form-item>
          <el-form-item style="text-align:center">
            <el-button type="primary" style="width: 200px;" @click="toTwo">下一步</el-button>
          </el-form-item>
        </el-form>
      </div>
      <div v-show="step === 2" v-loading="loading" class="step-card-two">
        <h3 class="step-card-two-header">
          构建对比矩阵
        </h3>
        <el-table :data="matrixArr" style="width: 90%; max-height: 500px; margin: 0 auto;">
          <!-- <el-table-column prop="" ></el-table-column> -->
          <el-table-column label=" " prop="name" />
          <el-table-column label="指标一" prop="one" />
          <el-table-column label="指标二" prop="two" />
          <el-table-column label="指标三" prop="three" />
          <el-table-column label="指标四" prop="four" />
          <el-table-column label="指标五" prop="five" />
        </el-table>
        <el-form style="margin-top: 40px;">
          <el-form-item style="text-align:center">
            <el-button-group>
              <el-button type="primary" style="width: 120px" icon="el-icon-arrow-left" @click="reOne">上一步</el-button>
              <el-button type="primary" style="width: 120px" @click="toThree">开始分析<i class="el-icon-arrow-right el-icon--right" /></el-button>
            </el-button-group>
          </el-form-item>
        </el-form>
      </div>
      <div v-show="step === 3" class="step-card-three">
        <h3>综合评估结果打分：80</h3>
        <div class="step-card-three-charts">
          <div id="charts" />
        </div>
        <el-form style="margin-top: 20px;">
          <el-form-item style="text-align:center">
            <el-button type="primary" style="width: 100px;" @click="reTwo">返回</el-button>
          </el-form-item>
        </el-form>
      </div>
    </el-card>
  </div>
</template>

<script>
export default {
  data() {
    return {
      options: [{
        value: '选项一',
        label: '选项一'
      }, {
        value: '选项二',
        label: '选项二'
      }, {
        value: '选项三',
        label: '选项三'
      }, {
        value: '选项四',
        label: '选项四'
      }, {
        value: '选项五',
        label: '选项五'
      }],
      formConfig: {
        target: '',
        checklist: ['准则层1'],
        selectOne: [],
        selectTwo: [],
        selectThree: [],
        selectFour: []
      },
      step: 1,
      matrixArr: [{
        name: '指标一',
        one: 1,
        two: 1,
        three: 1,
        four: 1,
        five: 1
      }, {
        name: '指标二',
        one: 1,
        two: 1,
        three: 1,
        four: 1,
        five: 1
      }, {
        name: '指标三',
        one: 1,
        two: 1,
        three: 1,
        four: 1,
        five: 1
      }, {
        name: '指标四',
        one: 1,
        two: 1,
        three: 1,
        four: 1,
        five: 1
      }, {
        name: '指标五',
        one: 1,
        two: 1,
        three: 1,
        four: 1,
        five: 1
      }],
      loading: false,
      option: {
        title: {
          text: ''
        },
        color: ['#409EFF'],
        tooltip: {
          trigger: 'axis',
          axisPointer: { // 坐标轴指示器，坐标轴触发有效
            type: 'shadow' // 默认为直线，可选为：'line' | 'shadow'
          }
        },
        grid: {
          left: '3%',
          right: '4%',
          bottom: '3%',
          containLabel: true
        },
        xAxis: [
          {
            type: 'category',
            data: ['指标一', '指标二', '指标三', '指标四', '指标五', '指标六', '指标七', '指标八', '指标九', '指标十'],
            axisTick: {
              alignWithLabel: true
            }
          }
        ],
        yAxis: [
          {
            type: 'value'
          }
        ],
        series: [
          {
            type: 'bar',
            barWidth: '60%',
            data: [20, 82, 91, 34, 90, 30, 31, 98, 64, 34]
          }
        ]
      },
      chart: null
    }
  },
  mounted() {
    this.initCharts()
  },
  methods: {
    initCharts() {
      this.chart = this.$charts.init(document.getElementById('charts'))
      this.chart.setOption(this.option)
    },
    toTwo() {
      this.step = 2
    },
    async toThree() {
      this.loading = true
      await setTimeout(() => {
        this.loading = false
        this.step = 3
        this.initCharts()
      }, 2000)
    },
    reTwo() {
      this.step = 2
    },
    reOne() {
      this.step = 1
    },
    testCheck(val) {
      return !this.formConfig.checklist.includes(val)
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
      margin: 25px 20px;
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
    .step-card {
      margin: 30px 20px;
      overflow: auto;
      &-one {
        width: 1000px;
        margin: 40px auto;
      }
      /deep/ .el-input{
        width: 390px;
      }
      &-two {
        width: 90%;
        margin: 40px auto;
        text-align: center;
      }
      &-three {
        h3 {
          text-align: center;
        }
        &-charts {
          width: 800px;
          min-height: 100px;
          margin: 0 auto;
          #charts {
            height: 400px;
            width: 700px;
            margin: 0 auto;
          }
        }
      }
    }
  }
</style>

