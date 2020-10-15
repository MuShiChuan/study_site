<template>

  <el-menu :default-active="activeIndex" class="el-menu-demo" mode="horizontal" @select="handleSelect">
    <el-menu-item index="1">
      <img width="370" height="44" src="./assets/logo.png" alt="延安大学西安创新学院精品课程网">
    </el-menu-item>
    <el-menu-item  v-popover:popover index="2">课程</el-menu-item>
    <el-popover
            ref="popover"
            placement="bottom-start"
            title=""
            width="760"
            trigger="hover">
      <CourseClassContainer></CourseClassContainer>
    </el-popover>
    <el-menu-item index="3"><a href="https://www.ele.me" target="_blank">学院</a></el-menu-item>
    <el-menu-item class="nav_right" index="4">
      <Login_register @setVisible="setVisible"></Login_register>
    </el-menu-item>
    <el-menu-item class="nav_right" v-if="visible" index="6"><a href="https://www.ele.me" target="_blank">个人中心</a></el-menu-item>
    <el-menu-item class="nav_right" index="5">
      <el-input id="input_search" placeholder="请输入内容" v-model="input3" class="input-with-select">
        <el-button slot="append" icon="el-icon-search"></el-button>
      </el-input>
    </el-menu-item>

  </el-menu>

</template>

<script>

import CourseClassContainer from "./components/CourseClassContainer";
import Login_register from "./components/login_register";
export default {
  name: 'App',
  data() {
    return {
      activeIndex: '1',
      input3: '',
      visible:false
    };
  },
  methods: {
    handleSelect() {
    },
    setVisible(visible){
      this.visible = visible
    }
  },
  components: {
    Login_register,
    CourseClassContainer
  }
}
</script>

<style>
  .el-menu--horizontal>.el-menu-item{
    border-bottom: none!important;
  }
  a{
    text-decoration: none;
  }
  .nav_right{
    float: right!important;
  }
  .el-input-group--append .el-input__inner, .el-input-group__prepend{
    border-top-left-radius:20px!important;
    border-bottom-left-radius: 20px!important;
  }
  .el-input-group--prepend .el-input__inner, .el-input-group__append{
    border-top-left-radius:20px!important;
    border-bottom-left-radius: 20px!important;
    border-top-right-radius:20px!important;
    border-bottom-right-radius: 20px!important;
    transform: translateX(-20px);
  }
  #input_search{
    border-color: rgb(179,192,209)
  }
</style>
