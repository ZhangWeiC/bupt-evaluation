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
      <div v-if="step === 1" class="step-card-one">
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
            <el-button type="primary" style="width: 200px;" @click="stepOne">下一步</el-button>
          </el-form-item>
        </el-form>
      </div>
      <div v-if="step === 2" class="step-card-two">
        <div class="step-card-two-header" />
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
      step: 1
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
    stepOne() {
      this.step = 2
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
      &-one {
        width: 1000px;
        margin: 40px auto;
      }
      /deep/ .el-input{
        width: 390px;
      }
    }
  }
</style>

