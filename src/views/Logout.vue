<template>
    <body id="poster">
    <el-form class="login-container" label-position="left" label-width="0px">
        <h3 class="login_title">系统登录</h3>
        <el-form-item>
            <el-input type="text" v-model="loginForm.username" auto-complete="off" placeholder="账号"></el-input>
        </el-form-item>

        <el-form-item>
            <el-input type="password" v-model="loginForm.password" auto-complete="off" placeholder="密码"></el-input>
        </el-form-item>

        <el-form-item style="width: 100%">
            <el-button type="primary" style="width: 100%;background: #505458;border: none" v-on:click="login">登录</el-button>
        </el-form-item>
    </el-form>
    </body>
</template>


<script>
    export default {
        name: "Logout",
        data() {
            return {
                loginForm: {
                    username: '',
                    password: ''
                },
                responseResult: []
            }
        },
        methods: {
            login() {
                const  _this= this
               axios
                    .post('http://192.168.1.155:9090/user/login?userName='+this.loginForm.username+"&password="+this.loginForm.password).then(function (resp) {

                       if(resp.data.code==='200'){
                           _this.$router.push('/')
                       }else{
                           const h = _this.$createElement;

                           _this.$notify({
                               title: '登录异常',
                               message: h('i', { style: 'color: teal'}, '登录失败，请稍后再试！')
                           });
                       }
                    })

            },
            open1() {
                const h = this.$createElement;

                this.$notify({
                    title: '标题名称',
                    message: h('i', { style: 'color: teal'}, '这是提示文案这是提示文案这是提示文案这是提示文案这是提示文案这是提示文案这是提示文案这是提示文案')
                });
            }
        }
    }
</script>

<style>
    #poster {
        /*background:url("../assets/eva.jpg") no-repeat;*/
        /*background-position: center;*/
        height: 100%;
        width: 100%;
        background-size: cover;
        position: fixed;
    }
    body{
        margin: 0px;
        padding: 0;
    }

    .login-container {
        border-radius: 15px;
        background-clip: padding-box;
        margin: 90px auto;
        width: 350px;
        padding: 35px 35px 15px 35px;
        background: #fff;
        border: 1px solid #eaeaea;
        box-shadow: 0 0 25px #cac6c6;
    }

    .login_title {
        margin: 0px auto 40px auto;
        text-align: center;
        color: #505458;
    }


</style>
