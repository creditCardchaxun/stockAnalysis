<template>
	<view>
		<view class="sticky">
			<view class="range-style mar-top">
				<view class="picker-title">名称:</view>
				<view class="picker_group">
					<uni-easyinput v-model="names" placeholder="请输入股票名称查询" clearable
						@change='getName'></uni-easyinput>
				</view>
			</view>
		</view>
		<view class="" style="height:50px;"></view>
		<view class="progress">
			<view class="weui-cells weui-cells_after-title">
				<view class="kecheng-nav">
					<text>名称</text><text>现价</text><text>买入价格</text><text>涨跌幅</text><text>操作</text>
				</view>
				<view class="kecheng" v-for="(item, index) in stockList" :key="index"
					@click.stop="lookdetails(item)">
					<view class='flexs-column'>
						<text>{{item.stocktitle}}</text>
						<text style="font-size: 12px;color:#8f939c">{{item.code}}</text>
					</view>
					<view>
						<text>{{item.currentPrice}}</text>
					</view>
					<view>
						<text>{{item.buyPrice}}</text>
					</view>
					<view>
					<uni-tag :text="item.advancers+'%'" type="error" />
					</view>
					<view class='flexs-column'>
						<view @click.stop="edit(item)" ><uni-tag text="修改" type="warning"/></view>
						<view @click.stop="remove(index)" style="margin-top: 5px;"><uni-tag text="删除"  /></view>
					
					</view>
	
				</view>
			</view> 
			 <!-- </view> -->
		</view>
		<view v-if="stockList.length == 0" style="text-align: center; padding-top: 20rpx">暂无数据</view>
		<view style="height: 55px"></view>
		<view class="btnGroup">
			<view class="button" @tap.stop.prevent="additem()">添加数据</view>
		</view>
	</view>
</template>


<script>
	export default {
		data() {
			return {
				stockList: [],
				page: 1,
				pageSize: 10,
				pageCount: 0,
				names: ''
			};
		},
		onShow() {
			this.stockList=JSON.parse(uni.getStorageSync('stockList'))
		},
		methods: {
			additem() {
				uni.navigateTo({
					url:"/pages/infomation/form"
				})
			},
			lookdetails(item){
				console.log(item)
				uni.navigateTo({
					url:'/pages/infomation/details?item='+ JSON.stringify(item)
				})
			},
			edit(item){
				uni.navigateTo({
					url:'/pages/infomation/form?item='+ JSON.stringify(item)
				})
			},
			remove(index){
				this.stockList.splice(index,1)
				uni.setStorageSync("stockList", JSON.stringify(this.stockList))
			},
			getName(){
				let arr=this.stockList.filter((ins,index)=>{
					return ins.stocktitle==this.names
				})
				this.stockList=arr
			}
			
		}
	}
</script>

<style>
	.sticky {
	    position: fixed;
	 /*   top:calc(44px + constant(safe-area-inset-top));
		top:calc(44px + env(safe-area-inset-top)); */
			/* #ifdef H5 */
				top:0;
			/* #endif */
	    left:0;
	    z-index: 9;
	    width: 100%;
	    background-color: #ef3037;
	    box-shadow: 0 0 10rpx #ef3037;
	    color: #4c4c4c; 
	}
	.range-style {
	    display: flex;
	    align-items: center;
	    padding-left: 10rpx;
	    background-color: #fff;
	}
	.mar-top {
	    /* margin-top: 30rpx; */
	    width: 95%;
	    margin-left: 15rpx;
	    margin-top: 10rpx;
	    margin-bottom: 10rpx;
	}
	.picker-title {
	    font-size: 28rpx;
	    width: 150rpx;
		text-align: center;
	}
	.picker_group {
	    color: #888;
	    /* border: 1rpx solid #A4A6AE; */
	    border-radius: 15rpx;
	    display: flex;
	    align-items: center;
	    justify-content: space-between;
	    /* padding: 20rpx 30rpx; */
	    font-size: 28rpx;
	    width: 80%;
	}
	.picker-title {
		width: 200rpx;
	}
	.kecheng{
		padding:10px 5px;
		display: flex;
		align-items: center;
		justify-content: space-around;
		border-bottom:1px solid #f5f5f5 ;
	}
	.kecheng-nav{
		display: flex;
		align-items: center;
		justify-content: space-around;
		border:1px solid #f5f5f5;
		padding:10px 5px;
	}
	.kecheng-nav text{
		color:#8f939c;
		/* padding:5px; */
	}
	
	.wisdom02 {
		font-size: 28rpx;
	}
	
	.wisdom02 view {
		line-height: 42rpx;
	}
	.progress{
		/* padding:10px; */
		/* width:100%; */
		background-color: #fff;
	}
	.progressTitle {
		display: flex;
		align-items: center;
	}
	
	.progressIcon {
		border: 1rpx solid #ddd;
		border-radius: 15rpx;
		padding: 0 10rpx;
	}
	
	.boldTitle {
		font-weight: bold;
		color: #000;
		margin-left: 10rpx;
	}
	
	.btnGroup {
		display: flex;
		align-items: center;
		width: 100%;
		height: 90rpx;
		position: fixed;
		bottom: 0;
		justify-content: space-between;
		background-color: #fff;
	}
	
	.button {
		width: 100%;
		background-color: #ef3037;
		text-align: center;
		line-height: 90rpx;
		color: #fff;
	}
	.flexs-column{
		display: flex;
		/* align-items: center; */
		flex-direction: column;
	}
</style>