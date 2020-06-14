<template>
  <div>
      <h3>Element Form</h3>
      <my-form :model="model" :rules="rules" ref="loginForm">
          <my-form-item label="用户名" prop="username">
              <my-input v-model="model.username" autocomplete="off" placeholder="请输入用户名"></my-input>
          </my-form-item>
          <my-form-item label="密码" prop="password">
              <my-input type="password" v-model="model.password" autocomplete="off"></my-input>
          </my-form-item>
          <my-form-item>
              <button type="button" @click="submitForm('loginForm')">提交</button>
          </my-form-item>
      </my-form>
  </div>
</template>
<script>
import MyForm from './form'
import MyFormItem from './form-item'
import MyInput from './input'

export default {
    name: 'Index',
    components: {
        MyForm,
        MyFormItem,
        MyInput
    },
    data() {
        return {
            model: {
                username: '',
                password: ''
            },
            rules: {
                username: [
                    { required: true, message: '请输入用户名' }
                ],
                password: [
                    { required: true, message: '请输入密码' }
                ]
            }
        }
    },
    methods: {
        submitForm(formName) {
            this.$refs[formName].validate(valid => {
                if (valid) {
                    alert('请求登录')
                } else {
                    alert('校验失败')
                    return false
                }
            })
        }
    }
}
</script>