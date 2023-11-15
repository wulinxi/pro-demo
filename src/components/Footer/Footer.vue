<template>
  <div class="footer-container">
    <!-- 全选 -->
    <div class="custom-control custom-checkbox">
        <input type="checkbox" class="custom-control-input" id="cbFull" :checked="isFull" @change="fullChange">
        <label class="custom-control-label" for="cbFull">全选</label>
    </div>
    <!-- 合计 -->
    <div>
        <span>合计：</span>
        <span class="total-price">￥{{ amount }}</span>
    </div>
    <!-- 结算按钮 -->
    <button type="button" class="btn btn-primary btn-settle">结算（{{all}}）</button>
  </div>
</template>

<script>
export default {
    name:"MyFooter",
    props:{
        //全选状态
        isFull:{
            type:Boolean,
            default:true
        },
        //总价格
        amount:{
            type:Number,
            default:0
        },
        //已勾选的数量
        all:{
            type:Number,
            default:0
        }
    },
    methods:{
        fullChange(e){
            //
			this.$emit('full-change',e.target.checked);
        }
    }
}
</script>

<style lang="less" scoped>
.footer-container{
    font-size: 14px;
    height: 50px;
    width: 100%;
    border-top: 1px solid #efefef;
    background-color: #fff;
    display: flex;
    align-items: center;
    justify-content: space-between;   
    position: fixed;
    bottom: 0;
    padding: 2px 10px;
}
.btn-settle{
    height: 80%;
    min-width: 100px;
    border-radius: 25px;
    font-size: 14px;
}
.total-price{
    color:red;
    font-weight: bold;
}
</style>