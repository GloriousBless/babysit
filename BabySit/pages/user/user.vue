<template>
	<view>
		<view v-if="!show_person">
			<view>
				<image src="../../static/anxinbeike.jpg" class="logo"></image>
				<view class="btn_login" @click="login()">
					<text>授权登录</text>
				</view>
			</view>
		</view>
		
		<view v-if="show_person">
			<view class="u-profile">
				<u-avatar
				       :src="headerUrl"
						size="200"
				    ></u-avatar>
			</view>
			
			
			<!-- 我的记录 -->
			<view class="remind">
				<view class="mine">我的记录</view>
				<view class="both">
					<view class="history">
						<text class="text1">历史浏览记录</text>
						<image src="../../static/user/button_right.png" class="img1"></image>
					</view>
					<view class="status">
						<text class="text2">宝贝情况记录</text>
						<image src="../../static/user/button_left.png" class="img2"></image>
					</view>
				</view>
			</view>
			
			<view class="item">
					<text class="concret">用户详情</text>
					<image src="../../static/user/right_arrow.png" class="arrow"></image>
			</view>
			<view class="item">
					<text class="concret">设置</text>
					<image src="../../static/user/right_arrow.png" class="arrow"></image>
			</view>
			<view class="item">
					<text class="concret">项目简介</text>
					<image src="../../static/user/right_arrow.png" class="arrow"></image>
			</view>
			<view class="item">
					<text class="concret">当前版本1.0.2</text>
					<image src="../../static/user/right_arrow.png" class="arrow"></image>
			</view>
			
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				show_person:false,
				list:[1,2,3,4,5],
				headerUrl:'https://pic4.zhimg.com/v2-018795ae154cf339fefab9fcdb7fdc7a_r.jpg?source=1940ef5c'
			}
		},
		// 没有箭头函数的指向问题，没有箭头指向的是uni.$on，而不是vm
		onLoad() {
			// uni.$on('loginSuccess',(show)=>{
			// 		this.show_person = show
			// 		console.log(this.show_person)
			// })
			
		},
		// onShow(){
		// 	uni.$on('avatar',(res)=>{
		// 				console.log('1111')
		// 	            this.headerUrl = res.headerUrl   //  为 B 页面传过来的值
		// 	        })
		// },
		onUnload() {
			 uni.$off('avatar')
		},
		methods: {
			login(){
				var that = this
				uni.showModal({
					title:'温馨提示',
					content:'授权微信登录后才能正常使用小程序功能',
					success(res){
						if(res.confirm){
							// uni.getUserProfile({
							// 	desc:'获取你的昵称和头像',
							// 	success:userRes=>{
							// 		if(userRes.errMsg == 'getUserProfile:ok' && userRes.userInfo != undefined){
							// 			var userInfo = {
							// 				avatarUrl: userRes.userInfo.avatarUrl,
							// 				nickName: userRes.userInfo.nickName
							// 			}
							// 			// 对变量进行赋值
							// 			that.nickName = userRes.userInfo.nickName
							// 			that.headerUrl = userRes.userInfo.avatarUrl
										
							// 			that.getUserOpenId(userInfo)
							// 			// console.log(that.nickName)
							// 			// console.log(that.headerUrl)
							
							setTimeout(function(){
								uni.switchTab({
									url:'/pages/StartPage/StartPage',
									success(){
										that.show_person = true
										uni.showToast({
											icon:'success',
											title:'登录成功'
										})
									}
								})
							},1000)
							
												
							
									
								}else if(res.cancel){}
								
							},fail: error =>{}
						
				})
			}
		}
	}
</script>

<style lang="scss" scoped>
	.logo{
		border-radius: 15rpx;
		width: 270rpx;
		height: 270rpx;
		margin-top: 180rpx;
		margin-left: 240rpx;
	}
	.btn_login{
		height: 100rpx;
		width: 220rpx;
		background-color: #28cc9e;
		margin-top: 100rpx;
		margin-left: 265rpx;
		border-radius: 20rpx;
		text-align: center;
		text{
			line-height: 100rpx;
			font-size: 35rpx;
			color: #ffffff;
			font-weight: bold;
		}
	}
	.u-demo-block__content{
		margin-top: 40%;
		margin-left: 30%;
	}
	.btn{
		margin-top: 100rpx;
		margin-left: 258rpx;
		width: 240rpx;
		height: 100rpx;
		background-color: #C0CDF9;
		border-radius: 20rpx;
		text-align: center;
		.text{
			line-height: 100rpx;
			font-size: 35rpx;
			color: white;
			font-family: 'heiti';
		}
	}
	.u-profile{
		margin-top: 15%;
		margin-left: 36%;
	}
	
	.remind{
		width: 90%;
		height: 200rpx;
		background-color: white;
		margin-top: 50rpx;
		border-radius: 15rpx;
		margin-left: 35rpx;
		.mine{
			height: 60rpx;
			font-size: 22rpx;
			font-weight: bolder;
			margin-left: 15rpx;
			padding-top: 15rpx;
			padding-left: 25rpx;
			letter-spacing: 1px;
		}
		.both{
			display: flex;
			width: 100%;
			height: 100rpx;
			justify-content: space-between;
			.history{
				display: flex;
				height: 100rpx;
				width: 45%;
				margin-left: 30rpx;
				border-radius: 15rpx;
				justify-content: space-between;
				background-image: linear-gradient( to right bottom , rgb(240,249,255) , #ffffff);
				.text1{
					font-size: 20rpx;
					width: 45%;
					height: 100rpx;
					padding-top: 15rpx;
					padding-left: 10rpx;
				}
				.img1{
					width: 50rpx;
					height: 50rpx;
					margin-right: 40rpx;
				}
			}
			.status{
				display: flex;
				height: 100rpx;
				width: 45%;
				border-radius: 15rpx;
				margin-right: 20rpx;
				justify-content: space-between;
				background-image: linear-gradient( to right bottom , rgb(238,240,252) , #ffffff);
				.text2{
					font-size: 20rpx;
					width: 45%;
					height: 100rpx;
					padding-top: 15rpx;
					padding-left: 10rpx;
				}
				.img2{
					width: 50rpx;
					height: 50rpx;
					margin-right: 40rpx;
				}
			}
		}
	}
	.item{
		display: flex;
		justify-content: space-between;
		width: 90%;
		height: 100rpx;
		background-color: #ffffff;
		border-radius: 15rpx;
		margin-left: 35rpx;
		margin-top: 25rpx;
		.concret{
			width: 50%;
			line-height: 100rpx;
			padding-left: 40rpx;
		}
		.arrow{
			width: 40rpx;
			height: 40rpx;
			margin-top: 30rpx;
			margin-right: 30rpx;
		}
	}
</style>
