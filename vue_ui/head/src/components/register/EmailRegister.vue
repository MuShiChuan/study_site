<template>
    <div>
        <div style="padding: 0 20px;width: 80%;margin: 0 auto">
            <el-form status-icon :rules="rules" class="demo-ruleForm" id="form" ref="form" :model="form" label-width="80px">
                <el-form-item prop="name" :label-width="formLabelWidth">
                    <el-input placeholder="常用邮箱" v-model="form.name" prefix-icon="el-icon-user-solid" clearable></el-input>
                </el-form-item>
                <el-form-item prop="password" :label-width="formLabelWidth">
                    <el-input placeholder="6 - 12 位密码，区分大小写" v-model="form.password" prefix-icon="el-icon-lock" show-password clearable></el-input>
                </el-form-item>
                <el-form-item prop="password1" :label-width="formLabelWidth">
                    <el-input placeholder="确认密码" v-model="form.password1" prefix-icon="el-icon-lock" show-password clearable></el-input>
                </el-form-item>
                <el-form-item style="margin-bottom: 0!important;" :label-width="formLabelWidth">
                    <el-button type="primary" @click="submitForm('form')">注册并登录</el-button>
                </el-form-item>

                <el-form-item prop="checked" :label-width="formLabelWidth">
                    <el-checkbox v-model="form.checked">
                        <div class="top">
                            <span>我同意</span>
                            <a href="">
                                《服务条款》
                            </a>
                            <span>和</span>
                            <a href="">
                                《隐私政策》
                            </a>
                        </div>

                    </el-checkbox>

                </el-form-item>
            </el-form>
        </div>
        <div class="bottom">
            <a @click.prevent="setComName" href="javascript:;">&lt;邮箱登录</a>
        </div>
    </div>
</template>

<script>
    export default {
        name: "EmailRegister",
        data(){
            var validatePass = (rule, value, callback) => {
                if (!/^\w{6,12}$/.test(value)) {
                    callback(new Error('密码必须6到12位'));
                } else {
                    if (this.form.password1 !== '') {
                        this.$refs.form.validateField('password1');
                    }
                    callback();
                }
            };
            var validatePass2 = (rule, value, callback) => {
                if (!/^[a-zA-Z]\w{5,11}$/.test(value)) {
                    callback(new Error('密码必须包含字母、数字、下划线，且以字母开头'));
                } else {
                    if (this.form.password1 !== '') {
                        this.$refs.form.validateField('password1');
                    }
                    callback();
                }
            };
            var validate2Pass2 = (rule, value, callback) => {
                if (value === '') {
                    callback(new Error('请再次输入密码'));
                } else if (value !== this.form.password) {
                    callback(new Error('两次输入密码不一致!'));
                } else {
                    callback();
                }
            };
            return{
                form: {
                    name: '',
                    password:'',
                    password1:'',
                    checked:false
                },
                rules: {
                    name: this.validator_rules.email,
                    password: [
                        {required: true, validator: validatePass, trigger: 'change'},
                        {required: true, validator: validatePass2, trigger: 'change'}
                    ],
                    password1: [{required: true, validator: validate2Pass2, trigger: 'change'}],
                    checked: this.validator_rules.checked
                },
                formLabelWidth: '0px'
            }
        },
        props:['validator_rules'],
        methods:{
            submitForm(formName) {
                this.$refs[formName].validate((valid) => {
                    if (valid) {
                        this.$emit('setLogin',true)
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
                this.$emit('setComName','Login')
            }
        },
    }
</script>

<style scoped>

</style>