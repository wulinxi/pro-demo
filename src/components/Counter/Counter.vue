<template>
	<div class="counter-container">
		<button type="button" class="btn btn-light btn-sm" @click="sub">-</button>
		<span class="number-box">{{num}}</span>
		<button type="button" class="btn btn-light btn-sm" @click="add">+</button>
	</div>
</template>

<script>
	import bus from '@/components/eventBus.js'
	export default{
		name:"Counter",
		props:{
			//接收id是为了方便后续的修改数量
			id:{
				required:true,
				type:Number
			},
			//接收数量
			num:{
				type:Number,
				default:1				
			}
		},
		methods:{
			sub(){
				if(this.num-1===0)return
				//要发送给App的数据格式{id,val}
				const obj={id:this.id,value:this.num-1}
				//发送数据
				bus.$emit("share",obj);
			},
			add(){
				
				//要发送给App的数据格式{id,val}
				const obj={id:this.id,value:this.num+1}
				//发送数据
				bus.$emit("share",obj);
			}
		}
	}
</script>

<style lang="less" scoped>
	.number-box{
		min-width: 30px;
		text-align: center;
		margin: 0 5px;
		font-size: 14px;
	}
	.btn-sm{
		width: 30px;
	}
</style>