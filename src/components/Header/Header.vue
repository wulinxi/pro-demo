<template>
    <div class="header-container">{{ title }}</div>
</template>

<script>
export default {
    name:"MyHeader",
    props:{
        //声明title自定义属性，允许使用者自定义标题内容
        title:{
            default:'购物车',
            type:String
        }
    }
    
}
</script>

<style lang="less">
.header-container{
    font-size: 14px;
    height: 50px;
    width: 100%;
    background-color: #0b74d6;
    display: flex;
    align-items: center;
    justify-content: center;
    color: #fff;
    position: fixed;
    top: 0;
    z-index: 9999;
}
</style>