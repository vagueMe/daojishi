<template>
  <div id="app">
    <el-tabs type="border-card">
      <el-tab-pane label="自定义">
        <el-row>
          <el-col :span="24" style="text-align: center">
            <el-button @click="add">添加</el-button>
          </el-col>
        </el-row>
        <br>
        <br>
        <el-row>
          <el-col v-for="(item, index) in timesArray" :key="index" :span="10" style="margin-bottom: 20px;margin-left: 20px;
        border-color: black;border-style:dashed;
      ">
            <TimesVue :allTimes="item.value" :title="item.title"/>
          </el-col>
        </el-row>
      </el-tab-pane>
      <el-tab-pane label="第二">
        <el-row>
          <el-col v-for="(item, index) in twoBarrier" :key="index" :span="index === 0 ? 20 : 10 " style="margin-bottom: 20px;margin-left: 20px;
              border-color: black;border-style:dashed;
            ">
            <TimesVue :allTimes="item.value" :title="item.title" :describe="item.describe" />
          </el-col>
        </el-row>
      </el-tab-pane>
      <el-tab-pane label="第三">
        <el-row>
          <span>瞬影</span><br>
          <span>灭影</span><br>
          <span>瞬影</span><br>
          <span style="color: red">居合斩</span><br>
          <span>灭影</span><br>
          <span>瞬影</span><br>
          <span>灭影</span><br>
          <span>瞬影</span><br>
          <span style="color: red">列光斩</span><br>
          <span>灭影</span><br>
          <span>瞬影</span><br>
          <span style="color: red">凌风斩</span><br>
          <span>灭影</span><br>
          <span>瞬影</span><br>
          <span style="color: red">居合斩</span><br>
          <span>灭影--技能放过后如果血量低于20% 直接<span style="color: red">列光斩</span></span><br>
          <span>瞬影</span><br>
          <span style="color: red">列光斩</span><br>
          <span>灭影</span><br>
          <span style="color: red">狂暴</span><br>
          <br><br><br>
          <span>大面向-游乐园-点名承伤+大黑洞-内外圈-游乐园-点名承伤+大黑洞-内外圈-游乐园-点名承伤+大黑洞-5S后狂暴</span>
        </el-row>
      </el-tab-pane>
      <el-tab-pane label="第四">
        <el-row style="text-align: center;font-size: 28px;">25%环形山</el-row>
        <el-row>
          <el-col v-for="(item, index) in fourBarrier" :key="index" :span="10" style="margin-bottom: 20px;margin-left: 20px;
        border-color: black;border-style:dashed;
      ">
            <TimesVue :allTimes="item.value" :title="item.title"/>
          </el-col>
        </el-row>
      </el-tab-pane>
    </el-tabs>



    <el-dialog
        title="提示"
        :visible.sync="dialogVisible"
        width="100%"
        style=""
        :before-close="handleClose">
        <el-form ref="ruleForm"   :rules="rules" label-position="right" label-width="80px" :model="formData">
          <el-form-item label="名称">
            <el-input v-model="formData.title"></el-input>
          </el-form-item>
          <el-form-item label="数字" required  prop="value">
            <el-input v-model.number="formData.value"></el-input>
          </el-form-item>
          <el-form-item style="text-align: center">
            <el-button type="primary" @click="ok('ruleForm')">确定</el-button>
            <el-button @click="cancel()">取消</el-button>
          </el-form-item>
        </el-form>
    </el-dialog>

  </div>
</template>

<script>
import TimesVue from './components/times-vue.vue'

export default {
  name: 'app',
  components: {
    TimesVue
  },
  data() {
    return {
      dialogVisible: false,
      formData: {},
      timesArray: [
      ],
      twoBarrier: [
        {title: "月华", value: 60},
        {title: "1号樱花", value: 50, describe: "90%出"},
        {title: "2号樱花", value: 50, describe: "70%出"},
        {title: "3号樱花", value: 50, describe: "45%出"},
        {title: "4号樱花", value: 50, describe: "20%出"},
      ],
      fourBarrier: [
        {title: "主投石", value: 35},
        {title: "主地动波", value: 30},
        {title: "左怪地动波", value: 30},
        {title: "右怪地动波", value: 30}
      ],
      rules: {
        value: [
          { required: true, message: '不能为空'},
          { type: 'number', message: '必须为数字值'}
        ],
      }
    }
  },
  mounted() {

  },
  methods: {
    add(){
      this.formData = {};
      this.dialogVisible = true;
      try {
        this.$refs['ruleForm'].resetFields();
        // eslint-disable-next-line no-empty
      } catch (error) {

      }

    },
    handleClose() {
      this.dialogVisible = false;
    },
    ok(formName) {
      this.$refs[formName].validate((valid) => {
        if (valid) {
          this.timesArray.push({
            title: this.formData.title,
            value: this.formData.value
          })
          this.dialogVisible = false;

        } else {
          console.log('error submit!!');
          return false;
        }
      });
    },
    cancel() {
      this.dialogVisible = false;
    }

  }
}
</script>

<style>
</style>
