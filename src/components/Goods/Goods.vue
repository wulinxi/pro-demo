<template>
	<div class="goods-container">
		<!-- 左侧图片区域 -->
		<div class="thumb">
			<div class="custom-control custom-checkbox">
				<input type="checkbox" class="custom-control-input" :id="'cb'+id" :checked="state" @change="stateChange">
				<label class="custom-control-label" :for="'cb'+id">
					<!-- 商品图 -->
					<img :src="pic" >
				</label>
			</div>
		</div>
		<!-- 右侧信息区域 -->
		<div class="goods-info">
			<!-- 商品标题 -->
			<h6 class="goods-title">{{title}}</h6>
			<div class="goods-info-bottom">
				<!-- 商品的价格 -->
				<span class="goods-price">￥{{price}}</span>
				<!-- 商品数量 -->
				<Counter :id="id" :num="count"></Counter>
			</div>
		</div>
	</div>
</template>

<script>
	import Counter from '@/components/Counter/Counter.vue'
	
	export default{
		name:"MyGoods",
		props:{
			//商品的id
			//为什么要封装一个id属性：原因就是将来子组件中的勾选状态变化之后，需要通过 子->父共享数据的形式
			//通知父组件根据id修改对应商品的勾选状态
			id:{
				required:true,
				type:Number
			},
			//标题
			title:{
				default:'',
				type:String
			},
			pic:{
				default:'',
				type:String
			},
			//单价
			price:{
				default:0,
				type:Number
			},
			//购买数量
			count:{
				default:1,
				type:Number
			},
			//商品勾选状态
			state:{
				default:true,
				type:Boolean
			}
		},
		methods:{
			//单选框改变事件
			stateChange(e){
				//
				const newState=e.target.checked;
				// console.log(newstate);
				//触发根组件App中自定义事件
				this.$emit('state-change',{id:this.id,value:newState})
				
			}
		},
		components:{
			Counter
		}
	}
</script>

<style lang="less" scoped>
.goods-container{
	padding: 10px;
	display: flex;
	.goods-container{
		border-top: 1px solid #efefef;
	}
	.thumb{
		display: flex;
		align-items: center;
		img{
			width: 100px;
			height: 100px;
			margin: 0 10px;
		}
	}
	.goods-info{
		display: flex;
		flex-direction: column;
		justify-content: space-between;
		flex: 1;
		.goods-title{
			font-weight: bold;
			font-size: 14px;
		}
	}
	.goods-info-bottom{
		display: flex;
		justify-content: space-between;
		.goods-price{
			font-weight: bold;
			color: red;
			font-size: 14px;
		}
	}
	
}
</style>