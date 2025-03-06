<template>
	<view class="container">
		<view class="main_track">
			<view class="example">
				<uni-forms ref="baseForm" :modelValue="baseFormData" label-width='100px'>
					<uni-forms-item label="股票名称" required name="stocktitle">
						<uni-easyinput v-model="baseFormData.stocktitle" placeholder="请输入股票名称" />
					</uni-forms-item>
					<uni-forms-item label="买入时间" required name="buyDate">
						<uni-datetime-picker type="date" return-type="string" v-model="baseFormData.buyDate"
							@change="dateChange" />
					</uni-forms-item>
					<uni-forms-item label="买入价格" required name="buyPrice">
						<uni-easyinput type='text' v-model="baseFormData.buyPrice" @input="calculateTotal"
							placeholder="请输入买入价格" />
					</uni-forms-item>
					<uni-forms-item label="买入数量" required name="buyNum">
						<uni-easyinput type='text' v-model="baseFormData.buyNum" @input="calculateTotal"
							placeholder="请输入买入股仓数量" />
					</uni-forms-item>
					<uni-forms-item label="今日涨跌幅" required name="advancers">
						<uni-easyinput type='text' v-model="baseFormData.advancers" 
							placeholder="请输入今日涨跌幅" />
					</uni-forms-item>
					<uni-forms-item label="买入总价格" required name="totalPrice">
						<uni-easyinput type='text' v-model="baseFormData.totalPrice" :disabled="true"
							placeholder="买入总价格=买入价格*买入数量" />
					</uni-forms-item>
					<uni-forms-item label="当日价格" required name='currentPrice'>
						<uni-easyinput type='text' v-model="baseFormData.currentPrice" placeholder="请输入当日价格" />
					</uni-forms-item>
					<uni-forms-item label="浮动盈亏金额" required name='fdPrice'>
						<uni-easyinput type='text' v-model="baseFormData.fdPrice" placeholder="请输入浮动盈亏金额" />
					</uni-forms-item>
					<uni-forms-item label="当日盈亏金额" required name='currtDatePrice'>
						<uni-easyinput type='text' v-model="baseFormData.currtDatePrice" placeholder="请输入当日盈亏金额" />
					</uni-forms-item>
					<uni-forms-item label="当日盈亏百分比" required name='dayPercent'>
						<uni-easyinput type='text' v-model="baseFormData.dayPercent" placeholder="请输入当日盈亏百分比" />
					</uni-forms-item>
					<uni-forms-item label="持仓盈亏百分比" required name='allPercent'>
						<uni-easyinput type='text' v-model="baseFormData.allPercent" placeholder="请输入持仓盈亏百分比" />
					</uni-forms-item>
					<uni-forms-item label="交易税费" required name='jysf'>
						<uni-easyinput type='text' v-model="baseFormData.jysf" placeholder="请输入交易税费" />
					</uni-forms-item>
				</uni-forms>
				<button type="primary" @click="submit('baseForm')">提交</button>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				// 基础表单数据
				baseFormData: {
					// stocktitle: '',
					// buyDate: '',
					// buyPrice: 0,
					// buyNum: 0,
					// currentPrice: 0,
					// fdPrice: 0,
					// currtDatePrice: 0,
					// totalPrice: 0,
					// days: '',
					// allPercent:0,
					// dayPercent:0,
					// advancers:0,
					// jysf:0,
					// ids:''
				},
				stockList:[],
				// details:{}
			}
		},
		onLoad(options) {
			console.log(options.item)
			// this.baseFormData={}
			this.stockList=JSON.parse(uni.getStorageSync('stockList'))
			let str=options.item?JSON.parse(options.item):{}
			this.baseFormData=str
			console.log(this.baseFormData)
		},

		methods: {
			calculateTotal() {
				this.baseFormData.totalPrice =Math.abs( Number(this.baseFormData.buyPrice) * Number(this.baseFormData.buyNum));
			},
			dateChange(e) {
				this.baseFormData.buyDate=e
				this.formatDate()
			},
			 formatDate() {
			 let currentDate = new Date();
			 let selectedDate = new Date(this.baseFormData.buyDate); // 用户选择的时间
			 let daysDifference = Math.abs(Math.ceil((selectedDate - currentDate) / (1000 * 60 * 60 * 24))); // 计算天数差
			 this.baseFormData.days=daysDifference
			 console.log('天数差:', daysDifference); // 输出天数差
			},
			submit(ref) {
				this.$refs[ref].validate().then(res => {
					  let data=this.baseFormData
					if(this.baseFormData.ids&&this.baseFormData.ids!=''){
						let arr= this.stockList
						for (let i = 0; i < arr.length; i++) {
						  if(arr[i].ids==this.baseFormData.ids){
						  	  arr[i]=data
						  }
						}
						 this.stockList=arr
					}else{
						data.ids=Math.floor(Math.random()*100)
						 this.stockList.push(data)
					}
				 setTimeout(()=>{
					  uni.setStorageSync("stockList", JSON.stringify(this.stockList))
					 uni.showToast({
						title:'提交成功',
						icon:'success'
					 })
					 this.baseFormData={}
					 uni.navigateBack()
				 },1000)
				
				}).catch(err => {
					console.log('err', err);
					uni.showToast({
						title:'提交失败',
						icon:'error'
					})
				})
			},
		}
	}
</script>

<style>
	.example {
		padding: 20px 0;
	}
</style>