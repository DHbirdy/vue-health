<template>
    <div class="login_container">
        <div class="login_box">
            <div class="avatar_box">
                <!--头像-->
                <img src="../assets/logo.png" alt />
            </div>
        <!-- 表单区域-->
            <el-form ref="loginFormRef" :model="loginForm" :rules="loginRules">
                <el-form-item  prop="username" label="用户名">
                    <el-input v-model="loginForm.username" prefix-icon="el-icon-user"></el-input>
                </el-form-item>
                <el-form-item  prop="password" label="密码">
                    <el-input v-model="loginForm.password" type="password" prefix-icon="el-icon-lock"></el-input>
                </el-form-item>
                <el-form-item class="btns">
                    <el-button type="primary" @click="submit">提交</el-button>
                    <el-button type="warning" @click="resetForm('loginFormRef')" >重置</el-button>
                </el-form-item>

             </el-form>
        </div>
    </div>


</template>

<script>
    export default {
        name: "Login",
        data(){
            return{
                loginForm:{
                    username: "admin",
                    password: "123456",
                },
                loginRules: {
                    username: [
                        {required: true, message: '请输入用户名必填项', trigger: 'blur'},
                        {min: 5, max: 12, message: '长度在 5 到 12 个字符', trigger: 'blur'}
                    ],
                    password: [
                        {required: true, message: '请输入密码必填项', trigger: 'blur'},
                        {min: 6, max: 12, message: '长度在 6 到 12 个字符', trigger: 'blur'}
                    ]
                },
            }
        },
        methods:{
            resetForm(formName){
                this.$refs[formName].resetFields();
            },
            submit(){
                //获取表单数据并验证
                this.$refs.loginFormRef.validate(async alid => {
                    if (!alid) return;
                    // 调用get请求
                    const {data :res} = await this.$http.post("test");
                    if (res == "health" ) {
                        window.sessionStorage.setItem('flag','ok'); // session 放置
                        this.$message.success("登录成功！！！");
                        // this.$router.push({ path: "/home"});
                    }else{
                        this.$message.error("登录失败！！！");
                    }
                });
            }
        }

    }
</script>

<style lang="less" scoped>

    .login_container{
        height: 100%;
        background: #2b4b6b;
    }
    .login_box {
        width: 450px;
        height: 300px;
        background-color: #fff;
        border-radius: 3px; // 圆角
        position: absolute; // 绝对定位
        left: 50%;
        top: 50%;
        transform: translate(-50%, -50%); // 根据自己位置 以自己为长度位移

        // 头像框
        .avatar_box {
            width: 130px;
            height: 130px;
            border: 1px solid #eee;
            border-radius: 50%; // 加圆角
            padding: 10px;
            box-shadow: 0 0 10px #ddd;// 盒子阴影
            position: absolute;
            left: 50%;
            transform: translate(-50%, -50%);
            background-color: #0ee;
            img {
                width: 100%;
                height: 100%;
                border-radius: 50%; // 加圆角
                background-color: #eee;
            }
        }
        .btns {
            display: flex;// 弹性布局
            justify-content: flex-end; // 尾部对齐
            /*position: relative;*/
            /*left: 50%;*/
            /*transform: translate(-50%, -50%);*/
        }
        .login_form {
            position: relative;
            width: 300px;
            top: 50px;
            padding: 50px 10px;

            box-sizing: border-box; // 设置边框

        }
    }

</style>