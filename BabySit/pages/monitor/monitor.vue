<template>
	<view>
		<scroll-view scroll-y>
			<view class="pic"></view>
			
				<view class="function">
					<view class="func">
						<view class="audio_shut_umbrella_other">
							<text class="text">播放白噪音</text>
							<u-switch v-model="value1" size="35" ></u-switch>
						</view>
						
						<view class="audio_shut_umbrella_other">
							<text class="text">自动安抚</text>
							<u-switch v-model="value2" size="35" ></u-switch>
						</view>
					</view>
					
					<view class="func">
						<view class="audio_shut_umbrella_other">
							<text class="text">遮阳罩</text>
							<u-switch v-model="value3" size="35" ></u-switch>
						</view>
						
						<view class="audio_shut_umbrella_other">
							<text class="text">摇晃风铃</text>
							<u-switch v-model="value4" size="35" ></u-switch>
						</view>
					</view>
					
					<view class="change_tem">
						<text class="text1">调节车垫温度</text>
						<image src="../../static/monitor/decrease.png" @click="decrease()"></image>
						<text class="text2">{{tempature}}</text>
						<image src="../../static/monitor/increase.png" @click="increase()"></image>
					</view>
					
				</view>
				
				<view class="pic2">
					<view class="txt">
						<text class="text">近期异常状态记录</text>
					</view>
					
					<view class="discri">
						<text class="time">时间</text>
						<text class="cry">哭闹</text>
						<text class="kick">踢被子</text>
						<text class="fever">发烧</text>
					</view>
					<baby-status v-for="(item,index) in statusData" :key="item.id" :item="item"></baby-status>
				</view>
				
				
		</scroll-view>
		
		<!-- 温度过高过低提示 -->
		 <quick-message ref="message"></quick-message>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				value1: true,
				value2: false,
				value3: true,
				value4: true,
				tempature:26,
				
				show_alert:false,
				statusData:[
					{
						id:1,
						time:'4-22 18:25:34',
						cry:'✔',
						kick:'✘',
						fever:'✘'
					},
					{
						id:2,
						time:'4-22 16:54:18',
						cry:'✘',
						kick:'✔',
						fever:'✘'
					},
					{
						id:3,
						time:'4-22 14:18:16',
						cry:'✘',
						kick:'✘',
						fever:'✘'
					},
					{
						id:4,
						time:'4-22 11:10:03',
						cry:'✔',
						kick:'✔',
						fever:'✘'
					},
					{
						id:5,
						time:'4-22 09:15:36',
						cry:'✘',
						kick:'✘',
						fever:'✘'
					},
					{
						id:6,
						time:'4-22 07:33:42',
						cry:'✘',
						kick:'✔',
						fever:'✘'
					},
					{
						id:7,
						time:'4-22 06:00:10',
						cry:'✘',
						kick:'✘',
						fever:'✘'
					},
					{
						id:8,
						time:'4-22 23:30:24',
						cry:'✔',
						kick:'✘',
						fever:'✔'
					}
				]
				
			}
		},
		methods: {
			decrease(){
				if(this.tempature > 20){
					this.tempature = this.tempature - 1
				}
				else{
					this.$refs.message.show({
					         type:'warning', //String 默认default
					         msg:'温度不能过低！', //String 显示内容 *
					         direction:'top', //String 默认顶部显示
					         icon:true, //Boolean|String 显示icon(false/true/string 默认显示icon)
					         mask:true, //Boolean 遮罩（默认false没有遮罩）
					         time:1000, //Number|Boolean 默认3000/false为不自动关闭
					         customStyle:{ //自定义样式
					                 color:'#FFFFFF', //字体图标色
					                 backgroundColor:'rgba(85, 170, 255, 0.5)' //背景色
					         }, 
					         iconSize: 16, //Number 自定义icon大小(单位px 默认16 设置后会覆盖自定义样式里的设置优先级最高)
					         iconColor: '', //String icon颜色(默认主题颜色 设置后会覆盖自定义样式里的设置优先级最高)
					    })
				}
			},
			increase(){
				if(this.tempature < 34){
					this.tempature = this.tempature + 1
				}
				else{
					this.$refs.message.show({
					         type:'warning', //String 默认default
					         msg:'温度不能过高！', //String 显示内容 *
					         direction:'top', //String 默认顶部显示
					         icon:true, //Boolean|String 显示icon(false/true/string 默认显示icon)
					         mask:true, //Boolean 遮罩（默认false没有遮罩）
					         time:1000, //Number|Boolean 默认3000/false为不自动关闭
					         customStyle:{ //自定义样式
					                 color:'#FFFFFF', //字体图标色
					                 backgroundColor:'rgba(255, 55, 68, 0.5)' //背景色
					         }, 
					         iconSize: 16, //Number 自定义icon大小(单位px 默认16 设置后会覆盖自定义样式里的设置优先级最高)
					         iconColor: '', //String icon颜色(默认主题颜色 设置后会覆盖自定义样式里的设置优先级最高)
					    })
				}
			},
		}
	}
</script>

<style lang="scss" scoped>
	.pic{
		background-color: #ffffff;
		height: 450rpx;
		width: 90%;
		margin: 50rpx 20rpx 20rpx 35rpx;
	}
	.function{
		background-color: #ffffff;
		border-radius: 15rpx;
		height: 420rpx;
		width: 90%;
		margin: 10rpx 20rpx 10rpx 35rpx;
		.func {
			height: 85rpx;
			margin: 20rpx 0rpx 10rpx 0rpx;
			display: flex;
			justify-content: space-around;
			.audio_shut_umbrella_other{
				margin-top: 20rpx;
				width: 33%;
				height: 85rpx;
				background-color: #D8D7FF;
				text-align: center;
				border-radius: 15rpx;
				display: flex;
				justify-content: space-around;
				.text{
					line-height: 85rpx;
				}
			}
		}
		.change_tem{
			width: 85%;
			height: 100rpx;
			display: flex;
			justify-content: space-around;
			margin: 80rpx 0rpx 10rpx 50rpx;
			border-radius: 15rpx;
			background-color: #D8D7FF;
			text{
				line-height: 100rpx;
			}
			.text2{
				font-size: 40rpx;
				font-weight: bold;
			}
			image{
				margin-top: 15rpx;
				height: 75rpx;
				width: 75rpx;
			}
		}
	}
	.pic2{
		background-color: #ffffff;
		height: 550rpx;
		width: 90%;
		border-radius: 15rpx;
		margin: 20rpx 20rpx 50rpx 35rpx;
		// padding-top: 10rpx;
		overflow:hidden;  //当父元素的padding为0时，内层的margin-top会给外层div使用
		.txt{
			width: 90%;
			height: 60rpx;
			border-radius: 15rpx;
			margin: 15rpx 10rpx 15rpx 35rpx;
			background-color: #D7D6FE;
			text-align: center;
			.text{
				
				line-height: 60rpx;
				font-size: 30rpx;
				font-weight: bold;
			}
		}
		.discri{
			width: 90%;
			height: 50rpx;
			font-family: 'STXinwei';
			.time{
				margin-left: 100rpx;
			}
			.cry{
				margin-left: 120rpx;
			}
			.kick{
				margin-left: 50rpx;
			}
			.fever{
				margin-left: 40rpx;
			}
		}
	}
</style>
