<template>
    <div style="display: inline-block;margin-right: 80px;">
        <el-button v-if="!isLogin" type="text" @click="dialogFormVisible = true">登录  |  注册</el-button>
        <el-dropdown v-else>
            <span class="el-dropdown-link">
                <el-avatar src="https://cube.elemecdn.com/0/88/03b0d39583f48206768a7534e55bcpng.png"></el-avatar>
                <i class="el-icon-arrow-down el-icon--right"></i>
            </span>
            <el-dropdown-menu slot="dropdown">
                <div>
                    <div class="dropdown-menu-title">
                        <div style="margin: 0 auto">正使用“手机”帐号登录</div>
                    </div>
                    <el-divider></el-divider>
                </div>
                <el-dropdown-item  ><a href="">设置</a></el-dropdown-item>
                <el-dropdown-item  ><a href="">课堂</a> </el-dropdown-item>
                <el-divider></el-divider>
                <el-dropdown-item  ><a href="">退出</a> </el-dropdown-item>
            </el-dropdown-menu>
        </el-dropdown>
        <el-dialog title="" :close-on-click-modal="false" id="dialog" :before-close="handleClose" :lock-scroll="false" :visible.sync="dialogFormVisible">
            <component @setLogin="setLogin" :validator_rules="validator_rules" @setComName="setComName" :visible="dialogFormVisible" :is="comName"></component>
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
            var validateChecked = (rule, value, callback) => {
                if (!value) {
                    callback(new Error('请先同意服务协议'));
                } else {
                    callback();
                }
            };

            return{
                dialogFormVisible: false,
                comName:'Login',
                isLogin:false,
                validator_rules:{
                    email:[
                        {type: 'string',required: true, message: '邮箱不能为空', trigger: 'change'},
                        {type: 'email',required: true, message: '邮箱格式不对', trigger: 'change'}
                    ],
                    phone:[
                        {
                            required: true,
                            pattern: /^(13[0-9]|14[5|7]|15[0|1|2|3|5|6|7|8|9]|18[0|1|2|3|5|6|7|8|9])\d{8}$/,
                            message: '手机号格式错误', trigger: 'change'
                        }
                    ],
                    password:[
                        { type: 'string', required: true,pattern:/^\w{6,12}$/ ,
                            message: '密码必须6到12位', trigger: 'change'},
                        { type: 'string', required: true,pattern:/^[a-zA-Z]\w{5,11}$/ ,
                            message: '密码必须包含字母、数字、下划线，且以字母开头', trigger: 'change'}
                    ],
                    account:[
                        { required: true,pattern: /^[a-zA-Z0-9_]{5,16}$/, message: '账号必须在5到16位', trigger: 'change'},
                        { required: true,pattern: /^[a-zA-Z][a-zA-Z0-9_]{4,15}$/, message: '账号必须包含字母、数字、下划线，且以字母开头', trigger: 'change'}
                    ],
                    checked:[{ required: true,validator: validateChecked, trigger: 'change'}]
                }
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
            },
            setLogin(isLogin){
                if(isLogin){
                    this.dialogFormVisible = !isLogin
                }
                this.isLogin = isLogin
                this.$emit('setVisible',isLogin)
            }
        },
        watch:{
            'comName':function () {
                if(this.comName==='EmailRegister'||this.comName==='PhoneRegister'||this.comName==='AccountRegister'){
                    document.getElementsByClassName('el-dialog__body')[0].style.padding='0 0 0 0'
                    var title = ''
                    if(this.comName==='EmailRegister'){
                        title = '邮箱注册<hr>'
                    }else if(this.comName==='PhoneRegister'){
                        title = '手机号注册<hr>'
                    }else if(this.comName==='AccountRegister'){
                        title = '账号注册<hr>'
                    }
                    document.getElementsByClassName('el-dialog__title')[0].innerHTML = title
                    document.getElementsByTagName('hr')[0].style.margin = '0'
                }else if(this.comName==='Login'){
                    document.getElementsByClassName('el-dialog__body')[0].style.padding='0px 20px 30px 20px'

                    document.getElementsByClassName('el-dialog__title')[0].innerHTML = ''
                }
            }
        },
        components:{
            Login,EmailRegister,PhoneRegister,AccountRegister
        }
    }
</script>

<style>
    .el-dialog__body{
        padding-top: 6px!important;
    }
</style>
<style scoped>
    >>> .el-input__inner{
        height: 50px;
    }
    >>> .bottom{
        height: 56px;
        background-color: #a3ff45;
        line-height: 56px;
        padding-left: 20px;
    }
    >>> .top{
        transform: translateY(-1px) !important;
    }
    >>> .el-button{
        width: 100%;
    }
    >>> form{
        padding-top: 10px;
    }
    .el-divider--horizontal{
        margin: 0;
    }
    .dropdown-menu-title{
        display: block;
        margin: 0 20px;
        text-align: center;
        margin-bottom: 10px;
        color: #B3C0D1;
        font-size: 14px;
    }
    .el-icon-arrow-down:hover{
        transform: rotate(180deg) ;
    }
    .el-dropdown-link:hover .el-icon-arrow-down{
        transform: rotate(180deg) ;
    }
    .el-icon-arrow-down{
        transition: all 0.8s ease-in-out;
    }
    a:hover{
        color: rgb(102,191,255);
    }
    a{
        color: rgb(96,98,102);
    }
</style>
<style>

</style>