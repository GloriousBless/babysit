<template>
	<view class="square">
		<view class="tab">
		<view>		
			<MySearch msg=""  input_border_color="#8ac6d1"
				input_bg_color="#fff" :inputValue="inputValue" 
				@input="handleInput" @search="search" class="mysearch">				
				<view class="forum" slot="left" >
						育儿论坛
				</view>
				<view slot="right">
					<u-icon name="search" size="32rpx" color="#999"></u-icon>
				</view>
			</MySearch>
		</view>

		<view class="main">
			<view class="item" style="margin: 20rpx 2rpx 2rpx 30rpx;" @click="healthy" :class="touch1==true ? 'active': ''"  @touchstart="start1()" @touchend="end1()">
				<image src="../../static/square/beauty.jpg"></image>
				<!-- <view class="block">靓丽宝贝</view>
				<view class="block_detail">晒出你家的宝贝吧</view> -->
			</view>
			<view class="item" style="margin: 20rpx 20rpx 2rpx 2rpx;" @click="healthy" :class="touch2==true ? 'active': ''"  @touchstart="start2()" @touchend="end2()">
				<image src="../../static/square/yinshi.jpg"></image>
				<!-- <view class="block">健康饮食</view>
				<view class="block_detail">身体倍倍棒</view> -->
			</view>
			<view class="item" style="margin: 2rpx 2rpx 20rpx 30rpx; " @click="healthy" :class="touch3==true ? 'active': ''"  @touchstart="start3()" @touchend="end3()">
				<image src="../../static/square/yufang.jpg"></image>
				<!-- <view class="block">疾病预防</view>
				<view class="block_detail">茁壮成长</view> -->
			</view>
			<view class="item" style="margin: 2rpx 20rpx 20rpx 2rpx;" @click="healthy" :class="touch4==true ? 'active': ''"  @touchstart="start4()" @touchend="end4()">
				<image src="../../static/square/qimeng.jpg"></image>
				<!-- <view class="block">启蒙计划</view>
				<view class="block_detail">养成好思想</view> -->
			</view>
		</view>
		
		<!-- 今日推荐部分 -->
		<view class="recommand">
			<view class="character">今日推荐</view>
			<u-icon name="arrow-right" color="#938AA9" size="28" class="forward"></u-icon>
		</view>
		</view>
		<scroll-view class="passage">
			<Recommand :item="item" v-for="(item,index) in NewList" :key="item.id"></Recommand>
			
		</scroll-view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				navIndex:0,
				touch1:false,
				touch2:false,
				touch3:false,
				touch4:false,
				NewList:[
					{
						id: 1,
						imgPath:"../../static/news/food.jpg", 
						title:"3岁宝宝食谱！科学！营养！",
						thumbs:"6.7万"
					},
					{
						id: 2,
						imgPath:"../../static/news/baby.jpg", 
						title:"婴儿黄疸病预防重点！",
						thumbs:"3.1万"
					},
					{
						id: 3,
						imgPath:"../../static/news/habit.jpg", 
						title:"教你让宝贝养成耐心的好习惯！",
						thumbs:"2.3万"
					},
					{
						id: 4,
						imgPath:"../../static/news/match.jpg", 
						title:"给宝宝更加营养的食物搭配！",
						thumbs:"4.5万"
					},
					{
						id: 5,
						imgPath:"../../static/news/happy.jpg", 
						title:"如何保持宝宝好心情！",
						thumbs:"2.7万"
					},
				]
			}
		},
		methods: {
			healthy(){
				uni.navigateTo({
					url:"/pages/Healty_diet/Healty_diet"
				})
			},
			start1(){
				this.touch1 = true
				console.log("111")
			},
			end1(){
				this.touch1 = false
			},
			start2(){
				this.touch2 = true
				console.log("111")
			},
			end2(){
				this.touch2 = false
			},
			start3(){
				this.touch3 = true
				console.log("111")
			},
			end3(){
				this.touch3 = false
			},
			start4(){
				this.touch4 = true
				console.log("111")
			},
			end4(){
				this.touch4 = false
			}
			
		}
	}
</script>

<style lang="scss" scoped>
	*{
		margin: 0;
		padding: 0;
	}
	.active{
		opacity: 0.7;
	}
	.square{
		
		.tab{
			position: fixed;
			z-index: 2;
			background-color: #dedcee;
		}
		.forum{
			flex: 1;
			color: #7A57D1;
			font-size: 60rpx;
			font-weight: bold;
			font-family: "STHupo";
			width: 300rpx;
		}
		.main{
			display: flex;
			flex-wrap: wrap;
			margin-left: 20rpx;
			margin-top: 20rpx;
			.item{
				width: 335rpx;
				height: 150rpx;
				background-repeat: no-repeat;
				background-size: 100% 100%;
				.block{
					margin: 10rpx 0rpx 0rpx 10rpx;
					font-size: 25rpx;
					font-weight: 600;
					color: #938AA9;
					font-family: SimHei;
					z-index: 2;
				}
				.block_detail{
					margin-left: 10rpx;
					font-size: 14rpx;
					color:#938AA9;
					font-family: SimHei;
				}
				image{
					z-index: -1;
					width: 100%;
					height: 100%;
				}
			}
			
		}
		.recommand{
			display: flex;
			background-color: #ffffff;
			white-space: nowrap;
			width: 89%;
			margin: 15rpx 18rpx 15rpx 45rpx;
			height: 80rpx;
			.character{
				margin-left: 20rpx;
				margin-right: 400rpx;
				color: #938AA9;
				line-height: 80rpx;
				font-size: 25rpx;
				font-weight: 600;
				font-family: SimHei;
			}
			.forward{
				margin-left: 100rpx;
			}
		}
		.passage{
			padding-top: 600rpx;
			
		}
	}
</style>
