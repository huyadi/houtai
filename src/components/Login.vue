<template>
  <div class="login-container">
    <div class="login">
      <!-- 头像 -->
      <div class="touxiang">
        <img src="../assets/1.jpeg" alt="" />
      </div>
      <!-- 表单 -->
      <el-form :model="loginFrom" :rules="rules" ref="myRef">
        <el-form-item prop="username">
          <el-input v-model="loginFrom.username" prefix-icon="iconfont icon-user"></el-input>
        </el-form-item>
        <el-form-item prop="password">
          <el-input type="password" v-model="loginFrom.password" prefix-icon="iconfont icon-lock_fill"></el-input>
        </el-form-item>
        <el-form-item>
          <el-button type="success" @click="login">登录</el-button>
          <el-button type="primary" @click="resetFrom">重置</el-button>
        </el-form-item>
      </el-form>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      loginFrom: {
        username: 'admin',
        password: '123456'
      },
      rules: {
        username: [
          { required: true, message: '请输入用户名称', trigger: 'blur' },
          { min: 3, max: 5, message: '长度在 3 到 5 个字符', trigger: 'blur' }
        ],
        password: [
          { required: true, message: '请输入密码', trigger: 'blur' },
          { min: 3, max: 10, message: '长度在 3 到 10 个字符', trigger: 'blur' }
        ]
      }
    }
  },
  created() {},
  mounted() {},
  methods: {
    // 重置表单
    resetFrom() {
      this.$refs.myRef.resetFields()
    },
    // 登录
    login() {
      this.$refs.myRef.validate(async valid => {
        if (!valid) return false
        const { data: res } = await this.http.post('login', this.loginFrom)
        console.log(res)
        if (res.meta.status !== 200) {
          return this.message.error('有错误')
        }

        this.message.success('登录成功')
        window.sessionStorage.setItem('token', res.data.token)
        this.$router.push('/home')
      })
    }
  }
}
</script>

<style lang="less" scoped>
.login-container {
  background-color: #2b4b6b;
  height: 600px;
  display: flex;
  align-items: center;
  justify-content: center;
}
.login {
  width: 450px;
  height: 300px;
  background-color: #fff;
  border-radius: 4px;
  position: relative;
  padding: 0 10px;
  .touxiang {
    position: absolute;
    left: 50%;
    transform: translate(-50%, -50%);
    width: 130px;
    height: 130px;
    border: 1px solid #eee;
    padding: 10px;
    border-radius: 50%;
    box-shadow: 0 0 10px #ddd;
    background-color: #fff;
    img {
      width: 100%;
      height: 100%;
      border-radius: 50%;
    }
  }
  .el-form {
    margin-top: 100px;
    text-align: right;
  }
}
</style>
