<template>
  <div id="login">
    <el-card class="box-card" shadow="always">
      <!-- 标题 -->
      <template #header>
        <div class="card-header">
          <span>登录</span>
        </div>
      </template>

      <el-form
        ref="ruleForm"
        :model="ruleForm"
        :rules="rules"
        label-position="left"
        size="small"
        label-width="90px"
        class="login-form"
      >
        <!-- 用户名 -->
        <el-form-item label="用户名:" prop="username">
          <div class="demo-input-suffix">
            <el-input
              ref="username"
              name="username"
              placeholder="用户名"
              v-model="ruleForm.username"
            >
              <i slot="prefix" class="el-input__icon el-icon-user"></i>
            </el-input>
          </div>
        </el-form-item>

        <!-- 密码 -->
        <el-form-item label="密码:" prop="password">
          <div class="demo-input-suffix">
            <el-input
              ref="password"
              name="password"
              placeholder="密码"
              v-model="ruleForm.password"
              :type="passwordType"
              :key="passwordType"
            >
            </el-input>
          </div>
        </el-form-item>

        <!-- 验证码 -->
        <el-form-item label="验证码:" prop="verifyCode" class="verify-input">
          <div class="demo-input-suffix">
            <el-input
              ref="verifyCode"
              placeholder="验证码"
              name="verifyCode"
              v-model="ruleForm.verifyCode"
            >
              <template slot="append">获取验证码</template>
            </el-input>
          </div>
        </el-form-item>

        <!-- 登录按钮 -->
        <el-button type="primary" size="small" style="width: 28%" class="login-button"
          >登录</el-button
        >
      </el-form>

      <el-divider></el-divider>

      <!-- 忘记密码和注册 -->
      <div class="clearfix">
        <el-link
          style="float: left"
          :underline="false"
          type="primary"
          class="link-left"
          >忘记密码</el-link
        >
        <el-link
          :underline="false"
          type="primary"
          class="link-right"
          @click="toRegister()"
          >注册</el-link
        >
      </div>
    </el-card>
  </div>
</template>

<script>
import { ref, reactive, toRefs } from "vue";
export default {
  name: "Login",
  setup(props, context) {
    console.log(props);
    console.log(context);
    console.log(this);

    const validateUsername = (rule, value, callback) => {
      if (value == null || value == "") {
        callback(new Error("用户名有误"));
      } else {
        callback();
      }
    };
    const validatePassword = (rule, value, callback) => {
      if (value.length < 2) {
        callback(new Error("密码有问题"));
      } else {
        callback();
      }
    };
    const validateVerifyCode = (rule, value, callback) => {
      if (value.length !== 4) {
        callback(new Error("验证码有误"));
      } else {
        callback();
      }
    };
    //登录信息
    const ruleForm = reactive({
      username: "410293095@qq.com",
      password: "wo123456789",
      verifyCode: "",
    });
    //表单验证
    const rules = reactive({
      username: [
        { required: true, trigger: "blur", validator: validateUsername },
      ],
      password: [
        { required: true, trigger: "blur", validator: validatePassword },
      ],
      verifyCode: [
        { required: true, trigger: "blur", validator: validateVerifyCode },
      ],
    });
    //input类型
    const passwordType = ref("password");

    const toRegister = () => {
      this.$router.push("/register");
    };

    return {
      ruleForm,
      rules,
      passwordType,
    };
  },
};
</script>

//element-ui的样式
<style>
.text {
  font-size: 14px;
}

.item {
  margin-bottom: 18px;
}

.clearfix:before,
.clearfix:after {
  display: table;
  content: "";
}
.clearfix:after {
  clear: both;
}

.box-card {
  width: 480px;
}
</style>

// 自定义样式
<style lang="scss" scoped>
#login {
  position: absolute;
  top: 50%;
  left: 50%;
  -webkit-transform: translate(-50%, -50%);
  -moz-transform: translate(-50%, -50%);
  -ms-transform: translate(-50%, -50%);
  -o-transform: translate(-50%, -50%);
  transform: translate(-50%, -50%);
}

.box-card {
  border: 1px solid #ccc;
}

.login-form {
  width: 75%;
  margin: auto;
  padding: 10px;
}

.login-button{
    margin: 0px auto 10px auto;
}

.link-left {
  float: left;
  padding: 10px;
}

.link-right {
  float: right;
  padding: 10px;
}
</style>

