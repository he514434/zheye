<template>
  <div class="container">
    <global-header :user="currentUser"></global-header>
      <form action="">
        <div class="mb-3">
          <label class="form-label">邮箱地址</label>
          <validate-input :rules="emailRules" v-model="emailVal"></validate-input>
        </div>
        <div class="mb-3">
          <label for="exampleInputEmail1" class="form-label">邮箱地址</label>
          <input
            type="text" class="form-control" id="exampleInputEmail1"
            v-model="emailRef.val"
            @blur="validateEmail"
          >
          <div class="form-text" v-if="emailRef.error">{{emailRef.message}}</div>
        </div>
        <div class="mb-3">
          <label for="exampleInputPassword1" class="form-label">密码</label>
          <input type="password" class="form-control" id="exampleInputPassword1">
        </div>
      </form>
    <column-list :list="columnList"></column-list>
  </div>
</template>

<script lang="ts">
import { defineComponent, reactive, ref } from 'vue'
import 'bootstrap/dist/css/bootstrap.min.css'
import ColumnList, { ColumnProps } from './components/ColumnList.vue'
import validateInput, { RulesProp } from './components/ValidateInput.vue'
import GlobalHeader, { UserProps } from './components/GlobalHeader.vue'
const emailReg = /^[a-zA-Z0-9.!#$%&’*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:\.[a-zA-Z0-9-]+)*$/
const testData: ColumnProps[] = [
  {
    id: 1,
    title: 'test1的专栏',
    description: '这是的test1专栏，有一段非常有意思的简介，可以更新一下欧',
    avatar: 'http://vue-maker.oss-cn-hangzhou.aliyuncs.com/vue-marker/5ee22dd58b3c4520912b9470.jpg?x-oss-process=image/resize,m_pad,h_100,w_100'
  },
  {
    id: 2,
    title: 'test2的专栏',
    description: '这是的test2专栏，有一段非常有意思的简介，可以更新一下欧',
    avatar: 'http://vue-maker.oss-cn-hangzhou.aliyuncs.com/vue-marker/5ee22dd58b3c4520912b9470.jpg?x-oss-process=image/resize,m_pad,h_100,w_100'
  },
  {
    id: 3,
    title: 'test3的专栏',
    description: '这是的test3专栏，有一段非常有意思的简介，可以更新一下欧'
    // avatar: 'http://vue-maker.oss-cn-hangzhou.aliyuncs.com/vue-marker/5ee22dd58b3c4520912b9470.jpg?x-oss-process=image/resize,m_pad,h_100,w_100'
  },
  {
    id: 4,
    title: 'test4的专栏',
    description: '这是的test4专栏，有一段非常有意思的简介，可以更新一下欧',
    avatar: 'http://vue-maker.oss-cn-hangzhou.aliyuncs.com/vue-marker/5ee22dd58b3c4520912b9470.jpg?x-oss-process=image/resize,m_pad,h_100,w_100'
  }
]
const currentUser: UserProps = {
  isLogin: true,
  name: 'kei'
}
export default defineComponent({
  name: 'App',
  components: {
    ColumnList,
    GlobalHeader,
    validateInput
  },
  setup () {
    const emailVal = ref('kei')
    const emailRules: RulesProp = [
      { type: 'required', message: '电子邮箱地址不能为空' },
      { type: 'email', message: '请输入正确的电子邮箱格式' }
    ]
    const emailRef = reactive({
      val: '',
      error: false,
      message: ''
    })
    const validateEmail = () => {
      if (emailRef.val.trim() === '') {
        emailRef.error = true
        emailRef.message = 'email不能为空'
      } else if (!emailReg.test(emailRef.val)) {
        emailRef.error = true
        emailRef.message = '请输入正确的email地址'
      }
    }
    return {
      columnList: testData,
      currentUser,
      emailRef,
      validateEmail,
      emailRules,
      emailVal
    }
  }
})
</script>

<style>

</style>
