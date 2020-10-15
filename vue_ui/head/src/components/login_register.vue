<template>
    <div style="display: inline-block;margin-right: 80px;">
        <el-button type="text" @click="dialogFormVisible = true">登录  |  注册</el-button>
        <el-dialog :close-on-click-modal="false" id="dialog" :before-close="handleClose" :lock-scroll="false" title="" :visible.sync="dialogFormVisible">
            <component @setComName="setComName" :visible="dialogFormVisible" :is="comName"></component>
        </el-dialog>
    </div>
</template>

<script>
    import Login from "./login/Login";

    import EmailRegister from "./register/EmailRegister";
    import PhoneRegister from "./register/PhoneRegister";
    import AccountRegister from "./register/AccountRegister";

    export default {
        name: "login_register",
        data(){
            return{
                dialogFormVisible: false,
                comName:'Login'
            }
        },
        methods:{
            handleClick() {
                // console.log(tab, event);
            },
            handleClose(done) {
                done()
                setTimeout(() => {
                    //代码
                    this.comName = 'Login'
                }, 500);

            },
            setComName(Name){
                // console.log(Name)
                this.comName = Name
            }
        },
        watch:{
            'comName':function () {
                if(this.comName==='EmailRegister'||this.comName==='PhoneRegister'||this.comName==='AccountRegister'){
                    document.getElementsByClassName('el-dialog__body')[0].style.padding='30px 0 0 0'
                }else {
                    document.getElementsByClassName('el-dialog__body')[0].style.padding='30px 20px 30px 20px'
                }
            }
        },
        components:{
            Login,EmailRegister,PhoneRegister,AccountRegister
        }
    }
</script>

<style scoped>
    >>> .el-input__inner{
        height: 50px;
    }
    >>> .bottom{
        height: 40px;
        background-color: #a3ff45;
        line-height: 40px;
        padding-left: 20px;
    }
</style>