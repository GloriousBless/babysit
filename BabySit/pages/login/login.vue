<template>
	<view>
		<view>
			<image src="../../static/anxinbeike.jpg"></image>
			<view class="btn" @click="login()">
				<text>授权登录</text>
			</view>
		</view>
	</view>
</template>

<script>
export default {
	data() {
		return {
			nickName:'',
			headerUrl:'',
			showPage:false
		}
	},
	methods: {
		// getUserOpenId(userInfo){
		// 	var that = this
		// 	uni.login({
		// 		provider:'weixin',
		// 		success(loginAuth){
		// 			var data = {'code': loginAuth.code}
		// 			let appid = 'wxe9bce482468a537d'
		// 			let secret = 'db3a2c34110ec94f09ccaf5d0c535be5'
		// 			let url = 'https://api.weixin.qq.com/sns/jscode2session?appid='+appid+'&secret='+secret+'&js_code='+loginAuth.code+'&grant_type=authorization_code';
					
		// 			uni.request({
		// 				url:url,
		// 				success:result =>{
							
		// 					uni.$emit('avatar',{headerUrl: that.headerUrl})
							           
		// 					console.info(that.headerUrl,that.nickName,result.data);
							
		// 					uni.switchTab({
		// 						url:'/pages/StartPage/StartPage',
		// 						success(){
		// 							uni.showToast({
		// 								icon:'success',
		// 								title:'登录成功'
		// 							})
		// 						}
		// 					})
		// 					uni.setStorageSync("openid",result.data.openid)
		// 					uni.getStorageSync("openid")
		// 				}
		// 			})
		// 		}
		// 	})
		// },
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
	
	
};
</script>

<style lang="scss" scoped>
	image{
		border-radius: 15rpx;
		width: 270rpx;
		height: 270rpx;
		margin-top: 180rpx;
		margin-left: 240rpx;
	}
	.btn{
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
</style>
