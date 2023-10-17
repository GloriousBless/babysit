<template>
	<view>
		<view class="page" :class="touch==true ? 'active': ''"  @touchstart="start()" @touchend="end()">
				<image :src="item.imgPath"></image>			
			<view>
				<view class="right">
					<view class="context">{{item.title}}</view>
					<view class="right_bottom">
						<u-icon name="heart" color="#252A34" size="35"></u-icon>
						<view class="praise">{{item.thumbs}}</view>
					</view>
					
				</view>	
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		name:"Recommand",
		props:['item'],
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
	.page{
		
		display: flex;
		margin: 15rpx 18rpx 15rpx 45rpx;
		width: 89%;
		height: 180rpx;
		border-radius: 10rpx;
		background-color: #ffffff;
			image{		
				width: 30%;
				height: 150rpx;
				margin: 12rpx;
			}
		.right{
			.context{
				font-size: 30rpx;
				font-weight: bold;
			}
			.right_bottom{
				display: flex;
				margin-top: 100rpx;
				margin-left: 320rpx;
				.praise{
					margin-left: 10rpx;
					font-weight: bold;
				}
			}
		}
	}
</style>