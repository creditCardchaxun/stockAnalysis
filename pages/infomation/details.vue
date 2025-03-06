<template>
	<view class="container">
			<uni-nav-bar :fixed="true" background-color="#ef3037" status-bar  color='#fff'>
				<block slot="left">
				      <view @click="goback"><uni-icons type="back" size="20" color="#fff"></uni-icons></view>
				     </block>
				<view style="display: flex;align-items: center;flex:1;justify-content: center;">
				<view @click="goback"><uni-icons type="back" size="20" color="#fff"></uni-icons></view>	
			
				<view style="display: flex;align-items: center;flex-direction: column;padding:0 10px;"> 
				<text style="font-size:16px">{{details.stocktitle}}</text> <text>现价 {{details.currentPrice}} {{details.advancers}}%</text>
				</view>
				<uni-icons type="forward" size="20" color="#fff"></uni-icons>
				</view>
				<view v-slot:right>
					<view class="">
						<uni-icons type="compose" size="20" color="#fff"></uni-icons>
						更多建仓
					</view>
				</view>
			</uni-nav-bar>
		<view class="main_track">
			<view class="profit-loss">
				<view>
					<view class="h1"> <text style="font-size: 14px;font-weight: 600;">浮动盈亏</text> <text
							style="font-size: 12px;color:#8f939c">{{details.buyDate}}-至今</text></view>
					<view class="value">+{{details.fdPrice}}</view>
					<view class="percentage">+{{details.allPercent}}%</view>
				</view>
				<view>
					<view class="h1"><text style="font-size: 14px;font-weight: 600;">当日盈亏参考</text> <uni-icons type="eye" size="20"></uni-icons></view>
					<view class="value">+{{details.currtDatePrice}}</view>
					<view class="percentage">+{{details.dayPercent}}%</view>
				</view>
			</view>
			<view class="details">
				<view class='d_01'>
					<text style="font-size: 12px;color:#8f939c">持股天数</text>
					<view style="font-weight: 600;">{{details.days}}</view>
				</view>
				<view class='d_01'>
					<text style="font-size: 12px;color:#8f939c">实现盈亏</text>
					<view style="font-weight: 600;">{{details.fdPrice}}</view>
				</view>
				<view class='d_01'>
					<text style="font-size: 12px;color:#8f939c">交易税费</text>
					<view style="font-weight: 600;">{{details.jysf}}</view>
				</view>
				<view class='d_01'>
					<text style="font-size: 12px;color:#8f939c">个股仓位</text>
					<view style="font-weight: 600;">42.5%</view>
				</view>
			</view>
		</view>
		<view class="details_con">
			<text style="font-size: 16px;font-weight: 600;">查看BS点</text>
			<text>
				<switch color="#ff0c24" style="transform:scale(0.8)" />
			</text>
		</view>
		<view class="main_track">
			<view class="transaction-record">
				<view class="record-01">
					<view class='h1'>交易记录</view>
					<view class="d-right">
						看行情<uni-icons type="eye" size="20"></uni-icons>
					</view>
				</view>
				<view class="record-02" style="padding-top: 15px;">
					<text style="color:#de3232;font-size: 16px;font-weight: 600;">建仓</text>
					<text style="font-weight: 600;padding-left:5px;">{{details.buyDate}}</text>
				</view>
				<view class="transaction-item">
					<text class='textfont'>价格</text>
					<text style="font-weight: 600;padding-left:20px;">{{details.buyPrice}}</text>
				</view>
				<view class="transaction-item">
					<text class='textfont'>数量</text>
					<text style="font-weight: 600;padding-left:20px;">{{details.buyNum}}</text>
				</view>
				<view class="transaction-item">
					<text class='textfont'>金额</text>
					<text style="font-weight: 600;padding-left:20px;">{{details.totalPrice}}</text>
				</view>
				<view class="transaction-item">
					<text class='textfont'>费用</text>
					<text style="font-weight: 600;padding-left:20px;">{{details.jysf}}</text>
				</view>
			</view>
		
		</view>
		<view class="details_con">
			<text style="font-size: 14px;font-weight: 600;width: 50%;text-align: center;border-right: 1px solid #eee;">添加笔记</text>
			<text style="font-size: 14px;font-weight: 600;width: 50%;text-align: center;">
				分享
			</text>
		</view>
		<view class='footer'>
			 <text>功能帮助</text><text>意见反馈</text>
		</view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				details:{}
			}
		},
		onLoad(options) {
			this.details=options.item?JSON.parse(options.item):{}
		},
		methods: {
           goback(){
			   uni.navigateBack({delta:1})
		   }
		}
	}
</script>

<style>



	.textfont {
		font-size: 14px;
		color: #8f939c;
	}

	.header {
		display: flex;
		justify-content: space-between;
		align-items: center;
		margin-bottom: 20px;
	}

	.heaviewr view {
		margin: 0;
		font-size: 24px;
	}

	.profit-loss {
		display: flex;
		justify-content: space-between;
		/* align-items: center; */
		padding: 15px 0;
	}

	.profit-loss .h1 {
		text-align: center;
		/* width: 50%; */
	}

	.profit-loss .value {
		font-size: 22px;
		color: #de3232;
		padding: 10px 0;
		font-weight: 600;
	}

	.profit-loss .percentage {
		font-size: 18px;
		color: #de3232;
		font-weight: 600;
		/* padding:2px 0; */
	}

	.details_con {
		/* border-top: 10px solid #f5f5f5;
		border-bottom: 10px solid #f5f5f5; */
		padding: 10px 20px;
		display: flex;
		justify-content: space-between;
		align-items: center;
		background-color: #fff;
	}

	.details {
		display: flex;
		justify-content: space-between;
		align-items: center;
		margin-bottom: 10px;
		flex-wrap: wrap;
		background-color: #fff;
	}

	.details .d_01 {
		text-align: center;
		width: 46%;
		display: flex;
		align-items: center;
		justify-content: space-between;
	}

	.record-02 {
		display: flex;
		align-items: center;
		padding: 8px 0;
	}

	.transaction-record {
		margin: 10px 0;
		overflow: hidden;
		padding:15px 0;
	}

	.record-01 {
		display: flex;
		justify-content: space-between;
		align-items: center;
	}

	.transaction-record .record-01 .h1 {
		font-size: 16px;
		font-weight: 600;
	}

	.transaction-item {
		width: 50%;
		float: left;
		display: flex;
		align-items: center;
	}
	.footer{
		    display: flex;
		    align-items: center;
		    justify-content: center;
			margin-top:10%;
	}
	.footer text{color:#6271ac;padding:0 20px;}
</style>