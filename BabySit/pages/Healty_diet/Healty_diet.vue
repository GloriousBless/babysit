<template>
	<view>
		<view class="tab">
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
			<view class="topic">
				<view class="t">
				健康饮食
				</view>
			</view>
			<view class="age">
				<view v-for="(item,index) in ageList " class="concrete_age" :key="index" :class="index==navIndex ? 'active': ''" @click="clickNav(index)">
					<view class="char">{{item.ages}}</view>
				</view>
			</view>
		</view>
		<scroll-view class="passage" >
			<Recommand :item="item" v-for="(item,index) in propelling[navIndex]" :key="item.only_id"></Recommand>
		</scroll-view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				navIndex: 0,
				propelling:[
					[
						{
							only_id:1,
							imgPath:"../../static/diet/breakfast.jpg",
							title:"3岁宝宝营养早餐分享",
							thumbs:"1.7万"
						},
						{
							only_id:2,
							imgPath:"../../static/diet/shipu.jpg",
							title:"2-3岁宝宝一周食谱参考",
							thumbs:"2.1万"
						},
						{
							only_id:3,
							imgPath:"../../static/diet/lunch.jpg",
							title:"3岁宝宝午餐.一周7天食谱",
							thumbs:"1.4万"
						},
						{
							only_id:4,
							imgPath:"../../static/diet/gaipian.jpg",
							title:"1岁以上宝宝钙片推荐",
							thumbs:"2639"
						},
						{
							only_id:5,
							imgPath:"../../static/diet/shipu.jpg",
							title:"2-3岁宝宝一周食谱参考",
							thumbs:"2.1万"
						},
						{
							only_id:6,
							imgPath:"../../static/diet/breakfast.jpg",
							title:"3岁宝宝营养早餐分享",
							thumbs:"1.7万"
						},
					],
					[	{
							only_id:1,
							imgPath:"../../static/diet/shipu.jpg",
							title:"2-3岁宝宝一周食谱参考",
							thumbs:"2.1万"
						},
						{
							only_id:2,
							imgPath:"../../static/diet/breakfast.jpg",
							title:"3岁宝宝营养早餐分享",
							thumbs:"1.7万"
						},
						{
							only_id:3,
							imgPath:"../../static/diet/lunch.jpg",
							title:"3岁宝宝午餐.一周7天食谱",
							thumbs:"1.4万"
						},
						{
							only_id:4,
							imgPath:"../../static/diet/gaipian.jpg",
							title:"1岁以上宝宝钙片推荐",
							thumbs:"2639"
						},
						{
							only_id:5,
							imgPath:"../../static/diet/gaipian.jpg",
							title:"1岁以上宝宝钙片推荐",
							thumbs:"2639"
						},
						{
								only_id:6,
								imgPath:"../../static/diet/shipu.jpg",
								title:"2-3岁宝宝一周食谱参考",
								thumbs:"2.1万"
							},
					],
					[
						{
							only_id:1,
							imgPath:"../../static/diet/gaipian.jpg",
							title:"1岁以上宝宝钙片推荐",
							thumbs:"2639"
						},
						{
							only_id:2,
							imgPath:"../../static/diet/lunch.jpg",
							title:"3岁宝宝午餐.一周7天食谱",
							thumbs:"1.4万"
						},
						{
							only_id:3,
							imgPath:"../../static/diet/shipu.jpg",
							title:"2-3岁宝宝一周食谱参考",
							thumbs:"2.1万"
						},
						{
							only_id:4,
							imgPath:"../../static/diet/lunch.jpg",
							title:"3岁宝宝午餐.一周7天食谱",
							thumbs:"1.4万"
						},
						{
							only_id:5,
							imgPath:"../../static/diet/gaipian.jpg",
							title:"1岁以上宝宝钙片推荐",
							thumbs:"2639"
						},
						{
							only_id:6,
							imgPath:"../../static/diet/breakfast.jpg",
							title:"3岁宝宝营养早餐分享",
							thumbs:"1.7万"
						},
					],
					[
						{
							only_id:1,
							imgPath:"../../static/diet/lunch.jpg",
							title:"3岁宝宝午餐.一周7天食谱",
							thumbs:"1.4万"
						},
						{
							only_id:2,
							imgPath:"../../static/diet/gaipian.jpg",
							title:"1岁以上宝宝钙片推荐",
							thumbs:"2639"
						},
						{
							only_id:3,
							imgPath:"../../static/diet/breakfast.jpg",
							title:"3岁宝宝营养早餐分享",
							thumbs:"1.7万"
						},
						{
							only_id:4,
							imgPath:"../../static/diet/shipu.jpg",
							title:"2-3岁宝宝一周食谱参考",
							thumbs:"2.1万"
						},
						{
							only_id:5,
							imgPath:"../../static/diet/gaipian.jpg",
							title:"1岁以上宝宝钙片推荐",
							thumbs:"2639"
						},
						{
							only_id:1,
							imgPath:"../../static/diet/lunch.jpg",
							title:"3岁宝宝午餐.一周7天食谱",
							thumbs:"1.4万"
						},
					]
				],
				ageList:[
					{
						id: 50,
						ages:"1月-12月"
					},
					{
						id: 51,
						ages:"2岁-3岁"
					},
					{
						id: 53,
						ages:"4岁-5岁"
					},
					{
						id: 54,
						ages:"6岁-12岁"
					},
				]
			}
		},
		methods: {
			clickNav(index){
				this.navIndex = index;
			}
		}
	}
</script>

<style lang="scss" scoped>
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
	.topic{
		font-size: 38rpx;
		font-weight: bolder;
		background-color: #ffffff;
		height: 60rpx;
		width: 90%;
		text-align: center;
		color: #8D7FA0;
		border-radius: 10rpx;
		margin: 25rpx 25rpx 25rpx 45rpx;
		justify-content: center;
		.t{
			line-height: 60rpx;
		}
	}
	.age{
		display: flex;
		flex-wrap: wrap;
		justify-content: space-around;
		width: 90%;
		height: 160rpx;
		margin: 25rpx 25rpx 25rpx 45rpx;
		background-color: #ffffff;
		border-radius: 10rpx;
		.concrete_age{
			height: 60rpx;
			width: 45%;
			text-align: center;
			background-color: #E3E4FF;
			margin: 10rpx 10rpx 10rpx 15rpx;
			.char{
				line-height: 60rpx;
				font-weight: bold;
			}
			&.active{
				background-color: #C1C7F9;
			}
		}
		.age:nth-child(2n){
			margin-left: 5rpx;
		}
	}
	.passage{
		padding-top: 400rpx;
	}
</style>
