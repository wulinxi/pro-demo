<template>
  <div class="app-container">
     <!-- 头部区域 -->
    <MyHeader title="购物车案例"></MyHeader>
    <!-- 内容部分 -->
    <MyGoods v-for="item in list" :key="item.id" :id="item.id" :title="item.goods_name" :pic="item.goods_img" :state="item.goods_state>0?true:false" :price="item.goods_price" :count="item.goods_count" @state-change="getNewState"></MyGoods>
    <!-- 底部区域 -->
    <MyFooter @full-change="getFullState" :isFull="fullState" :amount="amt" :all="total"></MyFooter>
  </div>
</template>

<script>
//导入组件
import MyHeader from '@/components/Header/Header.vue'
import MyFooter from '@/components/Footer/Footer.vue'
import MyGoods from '@/components/Goods/Goods.vue'

//导入axios请求库
import axios from 'axios'
import bus from '@/components/eventBus.js'

export default {
  name: 'App',
  data:function(){
    return {
		//用来存储查询的列表数据
      list:[]
    }   
  },
  //使用生命周期函数
  created(){
	  //调用请求数据的方法
	  this.initCartList();
	  
	  //接收count组件传递过来的数据
	  bus.$on('share',val=>{
		  this.list.some(item=>{
			  if(item.id===val.id){
				  item.goods_count=val.value
				  return true
			  }
		  })
		  console.log(val);
	  })
	  
  },
  methods:{
	  //封装请求列表数据的方法
	    async initCartList(){
		   //调用axios的个方法，请求列表数据
		 const {data:res} =await axios.get('http://wlhui.top:3002/demo-weekly/api/cart/list');
		 if(res.code==1){
			 //把查到的数据转存到data里的list数组
			 this.list=res.data
		 }
	   },
	   //接收子组件传递过来的数据
	   getNewState(e){
		   // console.log(e)
		   this.list.some(item=>{
			   if(item.id===e.id){
				   item.goods_state=e.value?1:0
				   //终止后面的循环
				   return true
			   }
		   })
		   
	   },
	   //接收footer子组件传递过来的全选按钮的状态
	   getFullState(val){
		   this.list.forEach(item=>(item.goods_state=val))
	   }
	   
  },
  //计算属性
  computed:{
	  //动态计算出全选的状态是true还是false
	  fullState(){
		  return this.list.every(item=>item.goods_state==1)?true:false;
	  },
	  //计算总价
	  amt(){
		  //filter 过滤 reduce 累加
		  return this.list.filter(item=>item.goods_state==1).reduce((total,item)=>(total+=item.goods_price*item.goods_count),0);
	  },
	  //计算总数
	  total(){
		  return this.list.filter(item=>item.goods_state==1).reduce((t,item)=>(t+=item.goods_count),0);
	  }
  },
  components:{
    MyHeader,
    MyFooter,
	MyGoods
  }
}
</script>

<style lang="less" scoped>
	.app-container{
		padding-top:50px;
		padding-bottom: 50px;
	}
</style>
