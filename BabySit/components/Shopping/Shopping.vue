<template>
	<view>
		<view class="shop" :class="touch==true ? 'active': ''"  @touchstart="start()" @touchend="end()">
			<image :src="item2.pic" class="img"></image>
			<view class="discription">{{item2.discription}}</view>
			<text class="ps">{{item2.ps}}万人收藏</text>
			<view class="money">
				<text class="cost">¥{{item2.cost}}</text>
				<text class="paid">{{item2.paid}}+人付款</text>
			</view>
			
			<view class="benefit">
				<view class="one">新品</view>
				<view class="two">24小时内发货</view>
				<view class="three">包邮</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		name:"Shopping",
		props:['item2'],
		data() {
			return {
				touch:false
			};
		},
		methods:{
			start(){
				this.touch = true
				console.log("111")
			},
			end(){
				this.touch = false
			}
		}
	}
</script>

<style lang="scss" scoped>
	.active{
		opacity: 0.7;
	}
	.shop{
		background-color: white;
		height: 470rpx;
		width: 330rpx;
		margin-left: 28rpx;
		margin-bottom: 25rpx;
		border-radius: 20rpx;
		.img{
			border-radius: 20rpx;
			width: 330rpx;
			height: 110px;
		}
		.discription{
			font-weight: bold;
			padding-left: 10rpx;
		}
		.ps{
			font-size: 20rpx;
			margin-left: 10rpx;
			color: #C4C2C7;
		}
		.money{
			display: flex;
			width: 100%;
			height: 40rpx;
			margin-top: 10rpx;
			margin-left: 10rpx;
			.cost{
				font-size: 35rpx;
				color: #F75A0C;
			}
			.paid{
				line-height: 40rpx;
				color: #C4C2C7;
				font-size: 18rpx;
				margin-left: 10rpx;
			}
		}
		.benefit{
			display: flex;
			width: 100%;
			height: 40rpx;
			margin-top: 20rpx;
			margin-left: 10rpx;
			.one{
				padding: 0;
				margin-right: 10rpx;
				border: 1rpx solid #EB7B53;
				font-size: 18rpx;
				width: 60rpx;
				line-height: 40rpx;
				text-align: center;
				color: #EB7B53;
				border-radius: 15rpx;
			}
			.two{
				padding: 0;
				border: 1rpx solid #C26687;
				font-size: 18rpx;
				width: 130rpx;
				border-radius: 15rpx;
				text-align: center;
				line-height: 40rpx;
				color: #C26687;
			}
			.three{
				margin-left: 10rpx;
				padding: 0;
				text-align: center;
				border: 1rpx solid #EB7B53;
				border-radius: 15rpx;
				font-size: 18rpx;
				width: 60rpx;
				line-height: 40rpx;
				color: #EB7B53;
			}
		}
	}
</style>