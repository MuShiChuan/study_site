<template>
    <div style="width: 80%;margin: 0 auto">
        <el-form status-icon class="demo-ruleForm" id="form" ref="form" :model="form" label-width="80px">
            <el-form-item
                    prop="name"
                    :rules="validator_rules.email"
                    :label-width="formLabelWidth">
                <el-input placeholder="常用邮箱" v-model="form.name" prefix-icon="el-icon-user-solid" clearable></el-input>
            </el-form-item>
            <el-form-item
                    prop="password"
                    :rules="validator_rules.password"
                    :label-width="formLabelWidth">
                <el-input placeholder="密码" v-model="form.password" prefix-icon="el-icon-lock" show-password clearable></el-input>
            </el-form-item>

            <el-form-item style="margin-bottom: 0!important;" :label-width="formLabelWidth">
                <el-button type="primary" @click="submitForm('form')">登录</el-button>
            </el-form-item>
            <span  @click="setComName">去注册</span>
        </el-form>
    </div>

</template>

<script>
    export default {
        name: "EmailLogin",
        data(){
            return{
                form: {
                    name: '',
                    password:''
                },
                formLabelWidth: '0px'
            }
        },
        props:['validator_rules'],
        methods: {
            submitForm(formName) {
                this.$refs[formName].validate((valid) => {
                    if (valid) {
                        this.$emit('setLogin',true)
                    } else {
                        console.log('error submit!!');
                        return false;
                    }
                });
            },
            resetForm(formName) {
                this.$refs[formName].resetFields();
                // this.$nextTick(()=>{
                // })
            },
            setComName(){
                this.$emit('setComName','EmailRegister')
            }
        }
    }
</script>

<style scoped>
    span{
        float: right;
        transform: translateY(-10px);
    }
</style>