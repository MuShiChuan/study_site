<template>
        <el-tabs :stretch="true" v-model="activeName" @tab-click="handleClick">
            <el-tab-pane label="邮箱登录" name="first">
                <EmailLogin @setLogin="setLogin" :validator_rules="validator_rules" @setComName="setComName"></EmailLogin>
            </el-tab-pane>
            <el-tab-pane label="手机号登录" name="second">
                <PhoneLogin @setLogin="setLogin" :validator_rules="validator_rules" @setComName="setComName"></PhoneLogin>
            </el-tab-pane>
            <el-tab-pane label="账号登录" name="third">
                <AccountLogin @setLogin="setLogin" :validator_rules="validator_rules" @setComName="setComName"></AccountLogin>
            </el-tab-pane>
        </el-tabs>
</template>

<script>
    import EmailLogin from "./EmailLogin";
    import PhoneLogin from "./PhoneLogin";
    import AccountLogin from "./AccountLogin";

    export default {
        name: "Login",
        data(){
            return{
                activeName: 'first',
            }
        },
        props:[
            'visible','validator_rules'
        ],
        methods:{
            handleClick(tab) {
                this.activeName = tab.name;
            },
            setComName(Name){
                this.$emit('setComName',Name)
            },
            setLogin(isLogin){
                this.$emit('setLogin',isLogin)
            }
        },
        watch:{
            'visible':function(newVal){
                if(!newVal){
                    if(this.activeName !== 'first'){
                        this.activeName = 'first'
                    }else {
                        this.$children[0].$children[1].$children[0].resetForm('form')
                    }
                }
            },
            'activeName':function (n,o) {
                // console.log(o + '---->' + n)
                var i = 0;
                (o==='first') ? (i = 1) :
                    (o==='second') ? (i = 2) :
                        ((o==='third')?(i = 3):i = 0);
                if(i!==0){
                    this.$children[0].$children[i].$children[0].resetForm('form')
                }
            }
        },
        components:{
            EmailLogin,AccountLogin,PhoneLogin
        }
    }
</script>

<style scoped>

</style>