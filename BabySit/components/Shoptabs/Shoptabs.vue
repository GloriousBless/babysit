<template>
	<view>
		<view class="tab_item">
			<image :src="item1.img_url" class="img"></image>
			<view class="char">{{item1.title}}</view>
		</view>
	</view>
</template>

<script>
	export default {
		name:"Shoptabs",
		props:['item1'],
		data() {
			return {
				
			};
		}
	}
</script>

<style lang="scss" scoped>
	.tab_item{
		background-color: white;
		border-radius: 10rpx;
		width: 132rpx;
		height: 128rpx;
		margin: 8rpx 5rpx 2rpx 5px;
		.img{
			width: 72rpx;
			height: 72rpx;
			margin-left: 24rpx;
			margin-top: 24rpx;
		}
		.char{
			text-align: center;
			margin-top: 4rpx;
			margin-bottom: 8rpx;
			font-size: 16rpx;
			font-weight: small;
			opacity: 0.75;
		}
	}
</style>