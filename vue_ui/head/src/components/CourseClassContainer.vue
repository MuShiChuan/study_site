<template>
    <div style="display: block!important;height: 420px">
        <div class="courseClassContainer">
            <h3 @click="m">课程大类</h3>
            <el-button style="margin: 10px 10px;width: 126px" v-bind:key="user.id" v-for="user in gridData" type="info">{{ user.name }}</el-button>
        </div>
    </div>
</template>

<script>
    import data from './CourseClassContainer.json'
    export default {
        name: "CourseClassContainer",
        data(){
            return {
                gridData: data.gridData1
            }
        },
        methods:{
            m(){
                console.log(data)
            }
        }
    }
</script>

<style scoped>
    .el-button{
        border-radius: 20px!important;
    }
    .courseClassContainer{
        padding: 10px;
        height: 400px;
        width: 740px;
        position:relative;
        overflow: auto;
    }
    .courseClassContainer::-webkit-scrollbar{
        width: 5px;
        background-color: rgba(193, 204, 186, 0.43);
    }
    .courseClassContainer::-webkit-scrollbar-thumb{
        -webkit-box-shadow: inset 0 0 6px rgba(0,0,0,.3);;
    }
</style>