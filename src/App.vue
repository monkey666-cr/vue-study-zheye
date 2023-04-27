<template>
  <div class="container">
    <global-header :user="currentUser"></global-header>
    <!-- <column-list :list="list"></column-list> -->

    <validate-form @form-submit="onFormSubmit">
      <div class="mb-3">
        <label for="exampleInputEmail1" class="form-label">邮箱地址</label>
        <validate-input :rules="emailRules" v-model="emailVal" class="hello there" placeholder="请输入邮箱地址"
          ref="inputRef"></validate-input>
      </div>
      <div class="mb-3">
        <label for="exampleInputPassword1" class="form-label">密码</label>
        <validate-input placeholder="请输入密码" type="password" :rules="passwordRules" v-model="passwordVal"></validate-input>
      </div>
      <div class="mb-3 form-check">
        <input type="checkbox" class="form-check-input" id="exampleCheck1">
        <label class="form-check-label" for="exampleCheck1">Check me out</label>
      </div>
      <template #submit>
        <span class="btn btn-danger">Submit</span>
      </template>
    </validate-form>

  </div>
</template>

<script lang="ts">
import { defineComponent, reactive, ref } from 'vue'
import 'bootstrap/dist/css/bootstrap.min.css'
import ColumnList, { ColumnProps } from './components/ColumnList.vue'
import GlobalHeader, { UserProps } from './components/GlobalHeader.vue'
import ValidateInput, { RulesProp } from './components/ValidateInput.vue'
import ValidateForm from './components/ValidateForm.vue'

const currentUser: UserProps = {
  isLogin: true,
  name: '陈润'
}

const testData: ColumnProps[] = reactive<ColumnProps[]>(
  [
    {
      id: 1,
      title: 'test1的专栏',
      description: '这里是test1专栏, 有一段非常有意思的简介, 可以更新一下哦'
    },
    {
      id: 2,
      title: 'test2的专栏',
      description: '这里是test2专栏, 有一段非常有意思的简介, 可以更新一下哦'
    },
    {
      id: 3,
      title: 'test3的专栏',
      description: '这里是test3专栏, 有一段非常有意思的简介, 可以更新一下哦'
    },
    {
      id: 4,
      title: 'test4的专栏',
      description: '这里是test4专栏, 有一段非常有意思的简介, 可以更新一下哦'
    },
    {
      id: 5,
      title: 'test5的专栏',
      description: '这里是test5专栏, 有一段非常有意思的简介, 可以更新一下哦'
    }
  ]
)

const emailReg = /^[a-zA-Z0-9.!#$%&’*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:\.[a-zA-Z0-9-]+)*$/

export default defineComponent({
  name: 'App',
  components: {
    // ColumnList,
    GlobalHeader,
    ValidateInput,
    ValidateForm
  },
  setup() {
    const emailRules: RulesProp = [
      { type: 'required', message: '电子邮箱地址不能为空' },
      { type: 'email', message: '请输入正确的电子邮箱格式' }

    ]
    const passwordRules: RulesProp = [
      { type: 'required', message: '密码不能为空' }
    ]
    const inputRef = ref<any>()
    const passwordVal = ref<string>()
    const onFormSubmit = (result: boolean) => {
      console.log(inputRef.value)
      console.log(123, result)
    }
    const emailVal = ref('chenrun')
    const emailRef = reactive({
      val: '',
      error: false,
      message: ''
    })
    const validateEmail = () => {
      if (emailRef.val.trim() === '') {
        emailRef.error = true
        emailRef.message = 'can not be empty'
      } else if (!emailReg.test(emailRef.val)) {
        emailRef.error = true
        emailRef.message = 'should be valid email'
      } else {
        emailRef.error = false
        emailRef.message = ''
      }
    }
    return {
      list: testData,
      currentUser: currentUser,
      emailRef,
      validateEmail,
      emailRules,
      emailVal,
      onFormSubmit,
      inputRef,
      passwordVal,
      passwordRules
    }
  }
})
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
