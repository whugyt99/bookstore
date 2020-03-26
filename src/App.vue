<template>
<div id="app">
<el-container>
<el-header>
<!--       登录按钮-->
<el-button type="text" @click="loginFormVisible = true" size="30px">登录</el-button>
<el-dialog style="text-align: left":visible.sync="loginFormVisible" title="登录账号" width="40%">
<el-form :label-position=labelPosition model="loginForm">
<el-form-item label="账号" :label-width="formLabelWidth">
<el-input v-model="loginForm.name" autocomplete="off"></el-input>
</el-form-item>
<el-form-item label="密码" :label-width="formLabelWidth">
<el-input type="password" v-model="loginForm.loginPass" autocomplete="off" ></el-input>
</el-form-item>
</el-form>
<div slot="footer" class="dialog-footer">
<el-button @click="loginFormVisible = false">取 消</el-button>
<el-button type="primary" @click="loginFormVisible = false">确 定</el-button>
</div>
</el-dialog>

<!--        //注册按钮-->
<el-button type="text" @click="registerFormVisible = true">注册</el-button>
<el-dialog style="text-align: left":visible.sync="registerFormVisible" title="注册账号" width="40%">
<el-form :model="registerForm" status-icon :rules="rules" ref="ruleForm" label-width="100px" class="demo-ruleForm">
<el-form-item label="手机号码" prop="phoneNumber">
<el-input v-model.number="registerForm.phoneNumber"></el-input>
</el-form-item>
<el-form-item label="密码" prop="pass">
<el-input type="password" v-model="registerForm.pass" autocomplete="off"></el-input>
</el-form-item>
<el-form-item label="确认密码" prop="checkPass">
<el-input type="password" v-model="registerForm.checkPass" autocomplete="off"></el-input>
</el-form-item>
<el-form-item>
<el-button @click="registerFormVisible = false">取 消</el-button>
<el-button type="primary" @click="submitForm('ruleForm')">提交</el-button>
<el-button @click="resetForm('ruleForm')">重置</el-button>
</el-form-item>
</el-form>
</el-dialog>
</el-header>
<el-main>
<el-menu :default-active="this.$route.path" class="el-menu-demo" router mode="horizontal" @open="handleOpen" @close="handleClose">
<el-menu-item v-for="(item,i) in navList" :key="i" >
  {{ item.navItem }}
</el-menu-item>
</el-menu>
<div>test</div>
</el-main>
</el-container>
    <router-view/>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
  var checkAge = (rule, value, callback) => {
  if (!value) {
  return callback(new Error('手机号不能为空'));
  }
  setTimeout(() => {
  if (!Number.isInteger(value)) {
  callback(new Error('请输入数字值'));}
  // } else {
  //   if (value.length !== 11) {
  //     callback(new Error('手机号格式不正确'));
  //   }
  else {
  callback();
  }
  }, 1000);
  };
  var validatePass = (rule, value, callback) => {
  if (value === '') {
  callback(new Error('请输入密码'));
  } else {
  if (this.registerForm.checkPass !== '') {
  this.$refs.ruleForm.validateField('checkPass');
  }
  callback();
  }
  };
  var validatePass2 = (rule, value, callback) => {
  if (value === '') {
  callback(new Error('请再次输入密码'));
  } else if (value !== this.registerForm.pass) {
  callback(new Error('两次输入密码不一致!'));
  } else {
  callback();
  }
  };
  return {
  activeName: 'second',
  labelPosition: 'top',
  loginFormVisible: false,
  registerFormVisible: false,
  loginForm: {
  count: '',
  loginPass: ''
  },
  formLabelWidth: '80px',
  navList: [
  {name: '/App', navItem: '推荐'},
  {name: '/components/HelloWorld', navItem: '教育'},
  {name: '/components/Novels', navItem: '小说'},
  {name: '/publishProject', navItem: '童书'},
  {name: '/personalCenter', navItem: '人文社科'},
  {name: '/components/Manager', navItem: '经管'},
  {name: '/components/Manager', navItem: '生活'},
  {name: '/components/Manager', navItem: '科技'},
  {name: '/components/Manager', navItem: '期刊'},
  ],
  registerForm: {
  pass: '',
  checkPass: '',
  phoneNumber: ''
  },
  rules: {
  pass: [
  { validator: validatePass, trigger: 'blur' }
  ],
  checkPass: [
  { validator: validatePass2, trigger: 'blur' }
  ],
  phoneNumber: [
  { validator: checkAge, trigger: 'blur' }
  ]
  }
  };
  },
  methods: {
  submitForm(formName) {
  this.$refs[formName].validate((valid) => {
  if (valid) {
  alert('submit!');
  } else {
  console.log('error submit!!');
  return false;
  }
  });
  },
  resetForm(formName) {
  this.$refs[formName].resetFields();
  },
  handleClick(tab, event) {
  console.log(tab, event);
  }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 0px;

  }

  .el-header, .el-footer {
  background-color: #B3C0D1;
  color: #333;
  text-align: right;
  line-height: 60px;
  }


  .el-main {
  background-color: #E9EEF3;
  color: #333;
  text-align: center;
  line-height: 60px;
  }

  body > .el-container {
  margin-bottom: 40px;
  }

  .el-container:nth-child(5) .el-aside,
  .el-container:nth-child(6) .el-aside {
  line-height: 260px;
  }

  .el-container:nth-child(7) .el-aside {
  line-height: 320px;
  }

  h1, h2 {
  font-weight: normal;
  }
  a {
  color: #42b983;
  }
</style>
