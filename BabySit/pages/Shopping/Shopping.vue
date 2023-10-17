<template>
	<!-- 这里的高度影响了swiper的高度 -->
	<view>
		<view>
			<view class="top_container">
				<view class="search_frame" >
					<u-input v-model="value" :type="text" :border="false" :height="60" :auto-height="true" class="search"/>
					<u-icon name="search" color="#000000" size="30"></u-icon>
				</view>
			</view>
		<view>
			<view class="tabs">
				<view class="tab">
					<u-tabs-swiper ref="uTabs" :list="list" :current="current" @change="tabsChange" :is-scroll="false"
							 swiperWidth="750" bg-color="#dedcee" active-color="#6a60a9"></u-tabs-swiper>
				</view>
			</view>
				<swiper :current="swiperCurrent" @transition="transition" @animationfinish="animationfinish" class="swiper-box">
					<swiper-item class="swiper-item1">
						<scroll-view scroll-y style="height: 100%; width: 100%;" class="scroll">
								<view class="sec_tabs">
									<Shoptabs :item1="item1" v-for="(item1, index1) in sec_tabs" :key="index1"></Shoptabs>
								</view>
								<!-- 商品 -->
								<view class="shop_item">
									<Shopping v-for="(item2,index2) in shop_items" :key="item2.id" :item2="item2"></Shopping>
								</view>
							</scroll-view>
					</swiper-item>
					
					<swiper-item class="swiper-item">
						<scroll-view scroll-y style="height: 100%; width: 100%;" class="scroll">
								<view class="sec_tabs">
									<Shoptabs :item1="item1" v-for="(item1, index1) in sec_tabs" :key="index1"></Shoptabs>
								</view>
								<!-- 商品 -->
								<view class="shop_item">
									<Shopping v-for="(item2,index2) in shop_items" :key="item2.id" :item2="item2"></Shopping>
								</view>
							</scroll-view>
					</swiper-item>
					
					<swiper-item class="swiper-item">
						<scroll-view scroll-y style="height: 100%; width: 100%;" class="scroll">
								<view class="sec_tabs">
									<Shoptabs :item1="item1" v-for="(item1, index1) in sec_tabs" :key="index1"></Shoptabs>
								</view>
								<!-- 商品 -->
								<view class="shop_item">
									<Shopping v-for="(item2,index2) in shop_items" :key="item2.id" :item2="item2"></Shopping>
								</view>
							</scroll-view>
					</swiper-item>
					
					<swiper-item class="swiper-item">
						<scroll-view scroll-y style="height: 100%; width: 100%;" class="scroll">
								<view class="sec_tabs">
									<Shoptabs :item1="item1" v-for="(item1, index1) in sec_tabs" :key="index1"></Shoptabs>
								</view>
								<!-- 商品 -->
								<view class="shop_item">
									<Shopping v-for="(item2,index2) in shop_items" :key="item2.id" :item2="item2"></Shopping>
								</view>
							</scroll-view>
					</swiper-item>
					
					<swiper-item class="swiper-item">
						<scroll-view scroll-y style="height: 100%; width: 100%;" class="scroll">
								<view class="sec_tabs">
									<Shoptabs :item1="item1" v-for="(item1, index1) in sec_tabs" :key="index1"></Shoptabs>
								</view>
								<!-- 商品 -->
								<view class="shop_item">
									<Shopping v-for="(item2,index2) in shop_items" :key="item2.id" :item2="item2"></Shopping>
								</view>
							</scroll-view>
					</swiper-item>
					
				</swiper>
				
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				scrollTop: 0,
				list: [{
					name: '全部'
				}, {
					name: '店铺'
				}, {
					name: '上新'
				},{
					name: '攻略'
				},{
					name: '关注'
				}],
				// 因为内部的滑动机制限制，请将tabs组件和swiper组件的current用不同变量赋值
				current: 0, // tabs组件的current值，表示当前活动的tab选项
				swiperCurrent: 0, // swiper组件的current值，表示当前那个swiper-item是活动的
				sec_tabs:[
					{
						title:'宝宝穿搭',
						img_url:'../../static/shop_sec_tab/pafu.png'
					},
					{
						title:'宝宝护肤',
						img_url:'../../static/shop_sec_tab/hufuru.png'
					},
					{
						title:'宝宝餐具',
						img_url:'../../static/shop_sec_tab/canju.png'
					},
					{
						title:'玩具',
						img_url:'../../static/shop_sec_tab/car.png'
					},
					{
						title:'奶瓶',
						img_url:'../../static/shop_sec_tab/naiping.png'
					},
					{
						title:'安抚娃娃',
						img_url:'../../static/shop_sec_tab/wawa.png'
					},
					{
						title:'安抚奶嘴',
						img_url:'../../static/shop_sec_tab/naizui.png'
					},
					{
						title:'早教绘本',
						img_url:'../../static/shop_sec_tab/huiben.png'
					},
					{
						title:'周岁礼服',
						img_url:'../../static/shop_sec_tab/lifu.png'
					},
					{
						title:'连体衣',
						img_url:'../../static/shop_sec_tab/liantiyi.png'
					}
				],
			shop_items:[
				{
					id:1,
					pic:"../../static/shop_object/pollow.jpg",
					discription:"婴儿睡眠巴布豆定型枕",
					ps:19.9,
					cost:49.9,
					paid:2000,
				},
				{
					id:2,
					pic:"../../static/shop_object/paper.jpg",
					discription:"舒适纸巾，婴儿适用",
					ps:20.8,
					cost:29.8,
					paid:1000,
				},
				{
					id:3,
					pic:"../../static/shop_object/towel.jpg",
					discription:"轻柔婴儿毛巾",
					ps:9.8,
					cost:21.9,
					paid:600,
				},
				{
					id:4,
					pic:"../../static/shop_object/toy.jpg",
					discription:"婴儿健身架",
					ps:3.2,
					cost:105,
					paid:300,
				}
				
			]
				
			};
		},
		onPageScroll(e) {
				this.scrollTop = e.scrollTop;
		},
		methods: {
			onPageScroll(e) {
					this.scrollTop = e.scrollTop;
				},
			// tabs通知swiper切换
			tabsChange(index) {
				this.swiperCurrent = index;
			},
			// swiper-item左右移动，通知tabs的滑块跟随移动
			transition(e) {
				let dx = e.detail.dx;
				this.$refs.uTabs.setDx(dx);
			},
			// 由于swiper的内部机制问题，快速切换swiper不会触发dx的连续变化，需要在结束时重置状态
			// swiper滑动结束，分别设置tabs和swiper的状态
			animationfinish(e) {
				let current = e.detail.current;
				this.$refs.uTabs.setFinishCurrent(current);
				this.swiperCurrent = current;
				this.current = current;
			},
			// scroll-view到底部加载更多
			onreachBottom() {
				
			},
			link(){
				console.log('1111')
			}
		}
	};
</script>

<style lang="scss" scoped>
	.top_container{
		position: fixed;
		z-index: 100;
		background-color: #dedcee;
		width: 100%;
		height: 80rpx;
		top:0;
		.search_frame{
			background-color: white;
			width: 90%;
			height: 60rpx;
			border-radius: 15rpx;
			margin-left: 30rpx;
			margin-top: 35rpx;
			display: flex;
			top: 0;
			// #ifndef MP-WEIXIN
			top: var(--status-bar-height);
			// #endif
			
			.search{
				width: 90%;
				line-height: 60rpx;
				margin-left: 23rpx;
			}
		}
	}
	.tabs{
		margin-top: 100rpx;
		.tab{
			background-color: #dedcee;
		}
		
	}
	.grid-text {
			font-size: 28rpx;
			margin-top: 4rpx;
			color: $u-type-info;
		}
	.sec_tabs{
		display: flex;
		margin-left: 5rpx;
		width: 820rpx;
		height: 300rpx;
		flex-direction: row;
		flex-wrap: wrap;
		margin-right: 23rpx;
		align-items: center;
		align-content: flex-start;
	}
	.swiper-box{
		height: calc(100vh - 180rpx);
	}
	.shop_item{
		display: flex;
		flex-wrap: wrap;
	}
</style>
