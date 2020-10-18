<template>
        <el-container class="home-container">

            <el-header>
                <div>
                    <img src="../assets/logo.png" class="logo_img"/>
                    <span>机票订单管理平台</span>
                </div>
                <el-button type="warning" @click="logout">安全退出</el-button>
            </el-header>
            <el-container>
                <el-aside width="200px">Aside</el-aside>
                <el-main>Main</el-main>
            </el-container>
        </el-container>
</template>

<script>
    export default {
        name: "Home",

        methods:{
            logout(){
                this.router.push("/login");
            }
        }
    }
</script>

<style lang="less" scoped>
    .home-container{
        height: 100%;
    }

    .el-header {
        background-color: #373d41;
        display: flex;
        justify-content: space-between;// 左右贴边
        padding-left: 0%;// 左边界
        align-items: center;// 水平
        color: #fff;
        font-size: 20px;
        > div { //左侧div加布局
            display: flex;
            align-items: center;
            span {
                 margin-left: 15px;
            }
        }
    }
    .logo_img {
        width: 55px;
        height: 55px;
    }
    .el-aside {
        background-color: #D3DCE6;
        color: #333;

    }

    .el-main {
        background-color: #E9EEF3;
        color: #333;

    }

</style>