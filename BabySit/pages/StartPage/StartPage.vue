<template>
	<view class="stastics">
		
		
		<view v-if="show">
			<image src="https://bpic.588ku.com/element_origin_min_pic/19/04/10/02c79f5bef42ba034c1fd84ffad28adf.jpg" height="300rpx" width="300rpx"></image>
		</view>
		
		
		<view v-if="!show">
			<view class="content" @click="useOutClickSide" >
					<easy-select ref="easySelect" size="medium" :value="selecValue" @selectOne="selectOne"></easy-select>
			</view>
			
			<!-- 宝宝 -->
			<scroll-view scroll-y class="baby">
				<view class="img">
					<image src="../../static/bigBaby.jpg" class="img" mode="aspectFill"></image>
				</view>
				<view class="condition">
					<view class="temperature_weight">
						<view class="tem1">宝贝体温</view>
						<view class="digit1">36.7℃</view>
							
					</view>
					<view class="environment_mood">
						<view>
							<view class="tem2">宝贝现在情绪</view>
							<image src="../../static/stastics/emoj.png" class="img"></image>
						</view>	
						
					</view>
				</view>
				
				<!-- 监控 -->
				<view class="monitor" :class="touch==true ? 'active2': ''"  @touchstart="start()" @touchend="end()" @click="monitor()">
					<text class="text">进入监控</text>
				</view>
				
				<view  class="position">
					<!-- <image src="../../static/position.jpg"></image> -->
					<map :latitude="lat" :longitude="lng" class="map" :markers="markers" scale="18" enable-3D></map>
				</view>
				
				
				
				<view class="baby_car">
					<view class="distance">相距：300米<text style="font-size: 22rpx;">(温馨提示：请保证婴儿车在您的视线范围内)</text></view>
					<view class="pos" @touchstart="changeColor1"  @touchend="changeColor2" :class=" act_color1==true ? 'active1':''">
						<text class="txt1">婴儿车当前位置</text>
						<text class="txt2">至诚路</text>
						<image src="../../static/stastics/sangejiantou.png"></image>
					</view>
					
					<view class="pos" @touchstart="changeColor3"  @touchend="changeColor4" :class=" act_color2==true ? 'active1':''">
						<text class="txt1">您当前所在位置</text>
						<text class="txt2">致志路</text>
						<image src="../../static/stastics/sangejiantou.png"></image>
					</view>
				</view>

				<view style="height: 20rpx;"></view>
			</scroll-view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				selecValue: '婴儿车1',
				act_color1:false,
				act_color2:false,
				touch:false,
				show:false,
				lat: 27.9047,
				lng:112.926406,
				markers:[
					{
						 id:0,
						latitude: 27.9047,//纬度
						longitude: 112.926406,//经度      
						rotate:0,   // 旋转度数
						width:20,   //宽
						height:30,   //高
							//   title:'我在这里',//标注点名
						alpha:0.8,   //透明度
						callout:{//自定义标记点上方的气泡窗口 点击有效  
						content:'至诚路',//文本
						color:'#6467EF',//文字颜色
						fontSize:12,//文本大小
						borderRadius:15,//边框圆角
						borderWidth:'10',
						bgColor:'#ffffff',//背景颜色
						display:'ALWAYS',//常显
						
						}
					
					},
					{
						 id:2,
						latitude: 27.90495,//纬度
						longitude: 112.926704,//经度      
						rotate:0,   // 旋转度数
						width:20,   //宽
						height:30,   //高
						iconPath:'../../static/yingerche.png',
					   //title:'我在这里',//标注点名
						alpha:0.8,   //透明度
						callout:{//自定义标记点上方的气泡窗口 点击有效  
						content:'致志路',//文本
						color:'#6467EF',//文字颜色
						fontSize:12,//文本大小
						borderRadius:15,//边框圆角
						borderWidth:'10',
						bgColor:'#ffffff',//背景颜色
						display:'ALWAYS',//常显
						}
					
					}
				]
			}
		},
		methods: {
			selectOne(options) {
			            this.selecValue = options.label
			        },
			        useOutClickSide() {
			            this.$refs.easySelect.hideOptions && this.$refs.easySelect.hideOptions()
			        },
					changeColor1(){
						this.act_color1 = true
					},
					changeColor2(){
						this.act_color1 = false
					},
					changeColor3(){
						this.act_color2 = true
					},
					changeColor4(){
						this.act_color2 = false
					},
					start(){
						this.touch = true
					},
					end(){
						this.touch = false
					},
					monitor(){
						uni.navigateTo({
							url:'/pages/monitor/monitor'
						})
					}
					
		}
	}
</script>

<style lang="scss" scoped>
	.active2{
		opacity: 0.7;
	}
	.home-wrap{
		.btn-box{
			width: 200rpx;
			margin: 100rpx auto;
		}
	}
	.baby{
		// 固定导航栏
		height: calc(100vh - 125rpx);
		.img{
			display: flex;
			justify-content: space-between;
			margin: 20rpx 20rpx 20rpx 30rpx;
			image{				
				height: 430rpx;
				width: 650rpx;			
				border-radius: 10rpx;
			}		 
		}
		.condition{
			display: flex;
			.temperature_weight{
				background-image: linear-gradient(to bottom right, #F1F0FF, #C3C3E5);
				width: 250rpx;
				height: 160rpx;
				margin: 20rpx 20rpx 20rpx 50rpx;
				border-radius: 10rpx;
				.tem1{
					padding: 10rpx;
					font-size: 25rpx;
					color: #6a60a9;
				}
				.digit1{
					font-size: 60rpx;
					font-weight: 400;
					text-align: center;
					color: #6a60a9;
				}
				
			}
			.environment_mood{
				background-image: linear-gradient(to top left ,  #c8e5e0, #d3cdff);
				width: 380rpx;
				height: 160rpx;
				margin: 20rpx 20rpx 20rpx 10rpx;
				border-radius: 10rpx;
				.tem2{
					padding: 20rpx 20rpx 0 20rpx;
					font-size: 25rpx;
					color: #6a60a9;
				}
				.img{
					margin-left: 160rpx;
					height: 80rpx;
					width: 80rpx;
				}
				
			}
		}
		.monitor{
			margin: 20rpx 50rpx 40rpx 50rpx;
			border-radius: 15rpx;
			height: 100rpx;
			width: 87%;
			background-color: #9DA6F5;
			text-align: center;
			.text{
				line-height: 100rpx;
				font-size: 40rpx;
				font-weight: bold;
			}
		}
		.position{
			
			margin: 20rpx 20rpx 60rpx 50rpx;
			height: 600rpx;
			width: 650rpx;
			.map{
				height: 600rpx;
				width: 650rpx;
			}
			// image{				
			// 	height: 850rpx;
			// 	width: 650rpx;			
			// 	border-radius: 15rpx;
			// }	
		}
		.baby_car{
			background-color: #ffffff;
			width: 650rpx;
			height: 300rpx;
			margin: 10rpx 20rpx 30rpx 50rpx;
			border-radius: 10rpx;
			.distance{
				padding: 50rpx 20rpx 10rpx 20rpx;
				
			}
			.active1{
				background-color: #EAEAEA;
			}
			.pos{
				display: flex;
				justify-content: space-between;
				margin: 25rpx 0 10rpx 0;
				font-size: 30rpx;
				height: 80rpx;
				image{
					height: 50rpx;
					width: 50rpx;
				}
				.txt1{
					padding-left: 25rpx;
				}
			}
		}
}
</style>
