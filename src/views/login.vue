<template>
    <div id="login">
        <h1 style="color: #fff;">企业信息管理系统</h1>
        <div class="login-box">
            <el-form ref="form" :model="form" label-width="80px" style="width: 100%; height: 100%;display: flex; flex-direction: column; align-items: center;justify-content: space-between;">
                <el-form-item label="角色:">
                    <el-radio-group v-model="form.role">
                        <el-radio label="销售人员"></el-radio>
                        <el-radio label="计划管理人员"></el-radio>
                        <el-radio label="财务部人员"></el-radio>
                        <el-radio label="仓库管理员"></el-radio>
                        <el-radio label="系统管理员"></el-radio>
                    </el-radio-group>
                </el-form-item>
                <el-form-item label="用户名:">
                    <el-input v-model="form.username" placeholder="请输入用户名"></el-input>
                </el-form-item>
                <el-form-item label="密码:">
                    <el-input v-model="form.password" placeholder="请输入密码" type="password"></el-input>
                </el-form-item>
                <el-form-item>
                    <el-button type="primary" @click="onSubmit">登录</el-button>
                    <el-button>注册</el-button>
                </el-form-item>
            </el-form>  
        </div>
    </div>
</template>
  
<script>
  export default {
    name: 'login',
    data: () => ({
        form: {
          username: '',
          password: '',
          role: '销售人员',
        }
    }),
    methods: {
      onSubmit() {
        console.log('submit!');
        this.$router.push('/home')
      }
    }
  }
</script>
  
<style scoped lang="scss">
    #login{
        width: 100vw;
        height: 100vh;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        background-image: url('./../assets/images/login1.jpg');
        background-size: cover;
        .login-box{
            width: 500px;
            height: 400px;
            background-color: red;
            border-radius: 5px;
            background-color: rgba(255, 255, 255, 0.7);
            ::v-deep .el-form{
                padding: 25px 15px 15px 5px;
                box-sizing: border-box;
                color: black;
                font-weight: bold;
                .el-form-item{
                    &:first-child{
                        margin-bottom: 0px;
                    }
                    &:last-child{
                        .el-form-item__content{
                            display: flex;
                            align-items: center;
                            justify-content: space-between;
                        }
                    }
                    width: 100%;
                    .el-radio-group{
                        .el-radio {
                            margin-bottom: 25px;
                        }
                    }
                }
            }
        }
    }
</style>
  