<template>
  <div>
    <el-form ref="formRef" :model="formData" :rules="rules" size="default" label-width="100px">
      <el-row gutter="15">
        <el-col :span="12">
          <el-form-item label="课程编号" prop="field102">
            <el-input v-model="formData.field102" type="text" placeholder="请输入课程编号" clearable
              :style="{width: '100%'}"></el-input>
          </el-form-item>
        </el-col>
        <el-col :span="12">
          <el-form-item label="下拉选择" prop="field103">
            <el-select v-model="formData.field103" placeholder="请选择下拉选择" clearable :style="{width: '100%'}">
              <el-option v-for="(item, index) in field103Options" :key="index" :label="item.label"
                :value="item.value" :disabled="item.disabled"></el-option>
            </el-select>
          </el-form-item>
        </el-col>
      </el-row>
      <el-row gutter="15">
        <el-col :span="12">
          <el-form-item label="单行文本" prop="field105">
            <el-input v-model="formData.field105" type="text" placeholder="请输入单行文本" clearable
              :style="{width: '100%'}"></el-input>
          </el-form-item>
        </el-col>
        <el-col :span="12">
          <el-form-item label="单行文本" prop="field106">
            <el-input v-model="formData.field106" type="text" placeholder="请输入单行文本" clearable
              :style="{width: '100%'}"></el-input>
          </el-form-item>
        </el-col>
      </el-row>
      <el-row gutter="15">
        <el-col :span="12">
          <el-form-item label="下拉选择" prop="field108">
            <el-select v-model="formData.field108" placeholder="请选择下拉选择" clearable :style="{width: '100%'}">
              <el-option v-for="(item, index) in field108Options" :key="index" :label="item.label"
                :value="item.value" :disabled="item.disabled"></el-option>
            </el-select>
          </el-form-item>
        </el-col>
        <el-col :span="12">
          <el-form-item label="时间范围" prop="field109">
            <el-time-picker v-model="formData.field109" is-range format="HH:mm:ss" value-format="HH:mm:ss"
              :style="{width: '100%'}" start-placeholder="开始时间" end-placeholder="结束时间" range-separator="至"
              clearable></el-time-picker>
          </el-form-item>
        </el-col>
      </el-row>
      <el-row gutter="15">
        <el-col :span="12">
          <el-form-item label="上传" prop="field113" required>
            <el-upload ref="field113" :file-list="field113fileList" :action="field113Action"
              :before-upload="field113BeforeUpload">
              <el-button size="small" type="primary" icon="el-icon-upload">点击上传</el-button>
            </el-upload>
          </el-form-item>
        </el-col>
        <el-col :span="12">
          <el-form-item label="评分" prop="field114">
            <el-rate v-model="formData.field114"></el-rate>
          </el-form-item>
        </el-col>
      </el-row>
      <el-row gutter="15">
        <el-form-item label="多行文本" prop="field116">
          <el-input v-model="formData.field116" type="textarea" placeholder="请输入多行文本"
            :autosize="{minRows: 4, maxRows: 4}" :style="{width: '100%'}"></el-input>
        </el-form-item>
      </el-row>
      <el-form-item>
        <el-button type="primary" @click="submitForm">提交</el-button>
        <el-button @click="resetForm">重置</el-button>
      </el-form-item>
    </el-form>
  </div>
</template>
<script setup>
import {
  ElMessage
}
from 'element-plus'
const formRef = ref()
const data = reactive({
  formData: {
    field102: undefined,
    field103: undefined,
    field105: undefined,
    field106: undefined,
    field108: undefined,
    field109: null,
    field113: null,
    field114: 0,
    field116: undefined,
  },
  rules: {
    field102: [{
      required: true,
      message: '请输入课程编号',
      trigger: 'blur'
    }],
    field103: [{
      required: true,
      message: '请选择下拉选择',
      trigger: 'change'
    }],
    field105: [{
      required: true,
      message: '请输入单行文本',
      trigger: 'blur'
    }],
    field106: [{
      required: true,
      message: '请输入单行文本',
      trigger: 'blur'
    }],
    field108: [{
      required: true,
      message: '请选择下拉选择',
      trigger: 'change'
    }],
    field109: [{
      required: true,
      message: '时间范围不能为空',
      trigger: 'change'
    }],
    field114: [{
      required: true,
      message: '评分不能为空',
      trigger: 'change'
    }],
    field116: [{
      required: true,
      message: '请输入多行文本',
      trigger: 'blur'
    }],
  }
})
const {
  formData,
  rules
} = toRefs(data)
const field103Options = ref([{
  "label": "选项一",
  "value": 1
}, {
  "label": "选项二",
  "value": 2
}])
const field108Options = ref([{
  "label": "选项一",
  "value": 1
}, {
  "label": "选项二",
  "value": 2
}])
// 上传请求路径
const field113Action = ref('https://jsonplaceholder.typicode.com/posts/')
// 上传文件列表
const field113fileList = ref([])
/**
 * @name: 上传之前的文件判断
 * @description: 上传之前的文件判断，判断文件大小文件类型等
 * @param {*} file
 * @return {*}
 */
function field113BeforeUpload(file) {
  let isRightSize = file.size / 1024 / 1024 < 2
  if (!isRightSize) {
    ElMessage.error('文件大小超过 2MB')
  }
  return isRightSize
}
/**
 * @name: 表单提交
 * @description: 表单提交方法
 * @return {*}
 */
function submitForm() {
  formRef.value.validate((valid) => {
    if (!valid) return
    // TODO 提交表单
  })
}
/**
 * @name: 表单重置
 * @description: 表单重置方法
 * @return {*}
 */
function resetForm() {
  formRef.value.resetFields()
}

</script>
<style>
.el-upload__tip {
  line-height: 1.2;
}

.el-rate {
  display: inline-block;
  vertical-align: text-top;
}

</style>
