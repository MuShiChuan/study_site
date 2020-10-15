<template>
    <div style="width: 80%;margin: 0 auto">
        <el-form class="demo-ruleForm" ref="form" :model="form" label-width="80px">
            <el-form-item
                    prop="name"
                    :rules="[
                      { required: true, message: '账号不能为空'}
                    ]"
                    :label-width="formLabelWidth">
                <el-input placeholder="账号" v-model="form.name" prefix-icon="el-icon-user" clearable></el-input>
            </el-form-item>
            <el-form-item
                    prop="password"
                    :rules="[
                      { required: true, message: '密码不能为空'}
                    ]"
                    :label-width="formLabelWidth">
                <el-input placeholder="密码" v-model="form.password" prefix-icon="el-icon-lock" show-password clearable></el-input>
            </el-form-item>

            <el-form-item style="margin-bottom: 0!important;" :label-width="formLabelWidth">
                <el-button type="primary" @click="submitForm('form')">登录</el-button>
            </el-form-item>
            <span @click="setComName">去注册</span>
        </el-form>
    </div>
</template>

<script>
    export default {
        name: "AccountLogin",
        data(){
            return{
                form: {
                    name: '',
                    password:''
                },
                formLabelWidth: '0px'
            }
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
            setComName(){
                this.$emit('setComName','AccountRegister')
            }
        }
    }
</script>

<style scoped>
    .el-button{
        width: 100%;
    }
    span{
        float: right;
        transform: translateY(-10px);
    }
    form{
        padding-top: 10px;
    }
</style>