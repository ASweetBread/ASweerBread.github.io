<script setup>
import { getStore } from '../../store';
import { useRoute } from 'vue-router'
import { computed } from '@vue/reactivity';

// 侧边栏控制
const asideBar = getStore()
function changeIsHide(){
    asideBar.changeHide()
}
// 用户图片
const imgsrc = "/src/assets/vue.svg"

// 面包屑导航
const route = useRoute()
const breadList = computed(()=>{
    return  route.matched.filter((item,index)=>index!==0&&item.meta.menuname)
})

</script>

<template>
<div class="navbar">
    <div class="collapse" @click="changeIsHide">
        <el-icon v-if="asideBar.isHide"><Expand /></el-icon> 
        <el-icon v-if="!asideBar.isHide"><Fold /></el-icon>
    </div>
    <div>
        <el-breadcrumb separator="/">
            <el-breadcrumb-item  :to="{ path: '/' }">首页</el-breadcrumb-item>
            <el-breadcrumb-item  :to="{ path: item.path }" v-for="item in breadList">{{item.meta.menuname}}</el-breadcrumb-item>
        </el-breadcrumb>
    </div>
    <div class="rightmenu">
        <div class="imgdiv">
            <el-dropdown placement="bottom">
                <img :src="imgsrc" alt="">
                <template #dropdown>
                    <el-dropdown-item>Action 1</el-dropdown-item>
                    <el-dropdown-item>Action 2</el-dropdown-item>
                    <el-dropdown-item>Action 3</el-dropdown-item>
                </template>
            </el-dropdown>
            
        </div>
        
    </div>
</div>
</template>

<style lang="scss" scoped>
.navbar {
    display: flex;
    align-items: center;
    height: 50px;
}
.collapse {
    margin-right: 24px;
    font-size: 20px;
    cursor: pointer;
    display: flex;
    align-items: center;
}
.rightmenu {
    margin-left: auto;
    display: flex;
    align-items: center;
}
.imgdiv {
    width: 40px;
    height: 40px;
    line-height: 40px; 
    border-radius: 50%;
    overflow: hidden;
    display: flex;
    align-items: center;
    justify-content: center;
    background-color: rgb(247, 247, 247);
    img {
        height: 100%;
        object-fit: cover;
    }
}



</style>
