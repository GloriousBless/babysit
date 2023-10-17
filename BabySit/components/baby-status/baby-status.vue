<template>
	<view>
		<view class="discri">
			<text class="time">{{item.time}}</text>
			<text class="cry">{{item.cry}}</text>
			<text class="kick">{{item.kick}}</text>
			<text class="fever" :class="item.fever=='✔' ? 'warn' : ''">{{item.fever}}</text>
		</view>
	</view>
</template>

<script>
	export default {
		name:"baby-status",
		props:['item'],
		data() {
			return {
				
			};
		}
	}
</script>

<style lang="scss" scoped>
	.discri{
		width: 90%;
		height: 50rpx;
		font-family: 'STXinwei';
		.time{
			margin-left: 30rpx;
		}
		.cry{
			margin-left: 100rpx;
		}
		.kick{
			margin-left: 100rpx;
		}
		.fever{
			margin-left: 90rpx;
		}
	}
	.warn{
		color: red;
		font-weight: bolder;
		font-size: 35rpx;
	}
</style>