<template>
  <div class="login">
    <!-- 放置一个el-card组件 -->
    <el-card class="login-card">
          <!-- 放置图片 -->
      <div class="title">
      <img src="../../assets/img/logo_index.png" alt="">
    </div>
    <!-- 放置表单 el-form model 绑定数据对象-->
    <el-form ref="myForm" :model="loginForm" :rules="loginRules">
      <!-- 表单里面  里面 prop要写要检验的字段名  放置 input/select/checkbox  相当于一行 -->
      <el-form-item prop="mobile">
        <el-input v-model="loginForm.mobile" placeholder="请输入手机号">
        </el-input>
      </el-form-item>
      <!-- 表单域 -->
      <el-form-item prop="code">
        <el-input v-model="loginForm.code" style="width:65%" placeholder="验证码"></el-input>
        <el-button plain style="float : right">验证码</el-button>
      </el-form-item>
      <el-form-item  prop="check">
        <!--复选框  -->
       <el-checkbox v-model="loginForm.check">我已阅读并同意用户协议和隐私条款</el-checkbox>
      </el-form-item>
      <el-form-item>
        <el-button @click="submitLogin"  type="primary" style="width:100%">登录</el-button>
      </el-form-item>
    </el-form>
    </el-card>
  </div>
</template>

<script>
export default {
  data () {
    return {
      loginForm: {
        mobile: '13911111111', // 手机号
        code: '246810', // 验证码
        check: false // 是否勾选，同意被坑
      },
      loginRules: {
        // 验证规则对象 key (字段名)： value(规则 => [])
        mobile: [{ required: true, message: '请输入你的手机号' }, {
          pattern: /^1[3456789]\d{9}$/, message: '手机号格式不正确'
        }],
        code: [{ required: true, message: '请输入你的验证码' }, {
          pattern: /^\d{6}$/, message: '验证码不正确'
        }],
        check: [{ validator: function (rule, value, callback) {
          // 自定义校验函数
          // rule 规则 没啥用
          // value 要校验的字段的值
          // callback 是一个回调函数
          if (value) {
            // 认为已经勾选
            callback() // 认为当前的规则校验通过了
          } else {
            // 认为没有勾选
            callback(new Error('你应该同意我们的霸王条款，无条件的接受我们欺负你')) // 如果没有勾选  认为当前校验失败  应该停止
          }
        } }]
      }
    }
  },
  methods: {
    submitLogin () {
    // 手动校验
      this.$refs.myForm.validate((isOK) => {
        if (isOK) {
          // 说明校验通过   应该用登录接口
          // console.log('校验通过，应该开始调用登录接口')
          // axios   body 参数  get 参数地址参数  路由参数  查询参数
          // body  参数  axios  data
          // get   参数   axious params
          console.log(this.loginForm)
          this.$axios({
            url: '/authorizations', // 请求地址 axios 没有指定 类型 默认是走get 类型
            method: 'post', // 类型
            data: this.loginForm // body  参数
          }).then(result => {
            // 直接受正确结果
            // 前端缓存
            window.localStorage.setItem('user-token', result.data.data.token)
            console.log(result)
          }).catch(() => {

          })
        }
      })
    }
  }
}

</script>

<style lang='less' scoped>
.login{
  background-image: url('../../assets/img/login_bg.jpg');
  height: 100vh;
    background-size: cover;
    display: flex;
    justify-content: center;
    align-items: center;
    .login-card {
      width: 440px;
      height: 350px;
      .title {
        text-align: center;
        margin-bottom: 30px;
        img {
          height: 45px;
        }
      }
    }
  }
</style>
