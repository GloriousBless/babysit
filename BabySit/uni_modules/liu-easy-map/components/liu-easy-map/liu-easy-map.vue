<template>
	<view style="width: 100%; height: 100%;">
		<map style="width: 100%; height: 100%;" id="esaymap" :scale="scale" :latitude="nowLat ? nowLat : centerLat"
			:longitude="nowLng ? nowLng : centerLng" :markers="markers" :polygons="polygonsData"
			:enable-zoom="isEnableZoom" :enable-scroll="isEnableScroll" :enable-satellite="isShowWxMap"
			:enable-rotate="isEnableRotate" @markertap="chooseItem" @tap="clickMap">
		</map>
		<view class="rightbox">
			<view class="boxitem" @click="changeTab(1)">
				<image class="itemimg" :src="tabIndex ? myaddressOnImg : myaddressImg" mode=""></image>
				<view class="itemname" :class="tabIndex ? 'active' : ''">我的位置</view>
			</view>
			<view class="boxitem" @click="changeTab(2)" v-if="wxMapShow">
				<image class="itemimg" :src="tabIndex2 ? wxmapOnImg:wxmapImg" mode=""></image>
				<view class="itemname" :class="tabIndex2 ? 'active' : ''">卫星地图</view>
			</view>
		</view>
		<cover-view class="detailbox" v-if="isShowDetail">
			<cover-image class="closeicon" :src="closeImg" @click="closeDetail"></cover-image>
			<cover-view class="boxl">
				<cover-view class="boxlhd">{{detailData.name || '--'}}</cover-view>
				<cover-view class="boxlbd">{{detailData.address || '--'}}</cover-view>
			</cover-view>
			<cover-view class="boxr" @click="goRoute">
				<cover-image class="boxrimg" :src="goImg" mode=""></cover-image>
			</cover-view>
		</cover-view>
	</view>
</template>

<script>
	export default {
		props: {
			//中心点纬度
			centerLat: {
				type: String,
				default: ''
			},
			//中心点经度
			centerLng: {
				type: String,
				default: ''
			},
			//标记点数据
			markerData: {
				type: Array,
				default () {
					return []
				}
			},
			//多边形数据
			polygons: {
				type: Array,
				default () {
					return []
				}
			},
			//标记点图标宽度
			markerIconWidth: {
				type: Number,
				default: 22
			},
			//标记点图标高度
			markerIconHeight: {
				type: Number,
				default: 32
			},
			//标记点图标路径
			markerIconUrl: {
				type: String,
				default: ''
			},
			//缩放级别 取值范围为3-20
			scale: {
				type: Number,
				default: 16
			},
			//是否显示指南针
			isShowCompass: {
				type: Boolean,
				default: false
			},
			//是否支持缩放
			isEnableZoom: {
				type: Boolean,
				default: true
			},
			//是否支持拖动
			isEnableScroll: {
				type: Boolean,
				default: true
			},
			//是否支持旋转
			isEnableRotate: {
				type: Boolean,
				default: false
			}
		},
		watch: {
			markerData: {
				immediate: true, //初始化的时候是否调用
				deep: true, //是否开启深度监听
				handler(newValue, oldValue) {
					this.markerData = newValue
				}
			},
			polygons: {
				immediate: true, //初始化的时候是否调用
				deep: true, //是否开启深度监听
				handler(newValue, oldValue) {
					this.polygonsData = [...newValue]
					console.log(this.polygonsData)
				}
			}
		},
		data() {
			return {
				markerImg: require('../../static/marker.png'),
				goImg: require('../../static/go.png'),
				myaddressImg: require('../../static/myaddress.png'),
				wxmapImg: require('../../static/wxmap.png'),
				myaddressOnImg: require('../../static/myaddress-on.png'),
				wxmapOnImg: require('../../static/wxmap-on.png'),
				closeImg: require('../../static/close.png'),
				polygonsData: [], //polygons区域数据
				markers: [], //markers数据
				detailData: {}, //选中展示详情数据
				nowLat: '', //我的当前位置
				nowLng: '',
				tabIndex: false,
				tabIndex2: false,
				isShowWxMap: false, //是否展示卫星地图 
				isShowDetail: false, //是否展示详情弹框
				wxMapShow: false, //是否展示卫星地图按钮（小程序展示）
			}
		},
		mounted() {
			const type = uni.getSystemInfoSync().uniPlatform
			if (type == 'mp-weixin') {
				this.wxMapShow = true
			}
			this.showMarkers()
			if (!this.centerLat || !this.centerLng) this.getLocation()
		},
		methods: {
			//右侧类型切换
			changeTab(index) {
				if (index == 1) {
					this.tabIndex = !this.tabIndex
					if (this.tabIndex) this.getLocation()
					else this.showMarkers()
				} else {
					this.tabIndex2 = !this.tabIndex2
					if (this.tabIndex2) this.isShowWxMap = true
					else this.isShowWxMap = false
				}
			},
			//获取当前的地理位置
			getLocation() {
				uni.getLocation({
					type: 'gcj02',
					isHighAccuracy: true,
					highAccuracyExpireTime: 3500,
					success: (res) => {
						this.nowLat = res.latitude
						this.nowLng = res.longitude
						let arr = [{
							id: 9999,
							latitude: res.latitude || '', //纬度
							longitude: res.longitude || '', //经度
							width: this.markerIconWidth, //宽
							height: this.markerIconHeight, //高
							iconPath: this.markerImg
						}];
						this.markers = [...arr];
						let mapObjs = uni.createMapContext('esaymap', this)
						mapObjs.moveToLocation({
							latitude: res.latitude,
							longitude: res.longitude
						}, {
							complete: res => {}
						})
					},
					fail: (res) => {
						if (res.errMsg == "getLocation:fail auth deny") {
							uni.showModal({
								content: '检测到您没打开获取信息功能权限，是否去设置打开？',
								confirmText: "确认",
								cancelText: '取消',
								success: (res) => {
									if (res.confirm) {
										uni.openSetting({
											success: (res) => {}
										})
									} else {
										return false;
									}
								}
							})
						}
					}
				})
			},
			//到这去
			goRoute() {
				uni.openLocation({
					latitude: +this.detailData.latitude,
					longitude: +this.detailData.longitude,
					scale: 17,
					name: this.detailData.address || '--',
					address: this.detailData.address || '--'
				});
			},
			//地图打点展示marker
			showMarkers() {
				if (this.markerData && this.markerData.length > 0) {
					var arr = []
					for (var i = 0; i < this.markerData.length; i++) {
						arr.push({
							id: Number(this.markerData[i].id),
							latitude: this.markerData[i].latitude || '', //纬度
							longitude: this.markerData[i].longitude || '', //经度
							iconPath: this.markerData[i].markerUrl ? this.markerData[i].markerUrl : this
								.markerImg, //显示的图标        
							rotate: 0, // 旋转度数
							width: this.markerData[i].iconWidth ? this.markerData[i].iconWidth : this
								.markerIconWidth, //宽
							height: this.markerData[i].iconHeight ? this.markerData[i].iconHeight : this
								.markerIconHeight, //高
							callout: { //自定义标记点上方的气泡窗口 点击有效
								content: this.markerData[i].name, //文本
								color: this.markerData[i].calloutColor || '#ffffff', //文字颜色
								fontSize: this.markerData[i].calloutFontSize || 14, //文本大小
								borderRadius: this.markerData[i].calloutBorderRadius || 6, //边框圆角
								padding: this.markerData[i].calloutPadding || 6,
								bgColor: this.markerData[i].calloutBgColor || '#0B6CFF', //背景颜色
								display: this.markerData[i].calloutDisplay || 'BYCLICK', //常显
							},
						})
					}
					this.markers = arr
				}
			},
			//点击标记点
			chooseItem(e) {
				let markerId = e.detail.markerId
				for (var i = 0; i < this.markerData.length; i++) {
					if (this.markerData[i].id == markerId) {
						this.isShowDetail = true
						this.detailData = this.markerData[i]
						this.$emit("clickMarker", this.markerData[i])
						break
					}
				}
			},
			//点击地图(仅微信小程序支持)
			clickMap(e) {
				// #ifdef MP-WEIXIN
				let lat = e.detail.latitude.toFixed(5)
				let lng = e.detail.longitude.toFixed(5)
				this.$emit("clickMap", {
					latitude: lat,
					longitude: lng
				})
				// #endif
			},
			//关闭详情弹框
			closeDetail() {
				this.detailData = {}
				this.isShowDetail = false
			}
		}
	}
</script>

<style>
	.rightbox {
		padding: 0 18rpx;
		background: #FFFFFF;
		box-shadow: 0rpx 4rpx 8rpx 0rpx rgba(200, 200, 200, 0.5);
		border-radius: 14rpx;
		position: fixed;
		top: 154rpx;
		right: 24rpx;
	}

	.boxitem {
		display: flex;
		flex-direction: column;
		text-align: center;
		padding-bottom: 8rpx;
		border-bottom: 2rpx solid #E4E4E4;
	}

	.itemimg {
		width: 40rpx;
		height: 40rpx;
		margin: 16rpx auto 4rpx;
	}

	.itemname {
		font-size: 24rpx;
		font-weight: 400;
		color: #333333;
		line-height: 42rpx;
	}

	.active {
		color: #2765F1;
	}

	.detailbox {
		display: flex;
		align-items: center;
		justify-content: space-between;
		width: calc(100% - 128rpx);
		padding: 24rpx 32rpx;
		background: #FFFFFF;
		border-radius: 16rpx;
		position: fixed;
		bottom: 32rpx;
		left: 32rpx;
	}

	.closeicon {
		width: 40rpx;
		height: 40rpx;
		position: absolute;
		right: 16rpx;
		top: 12rpx;
	}

	.boxl {
		width: calc(100% - 84rpx);
	}

	.boxlhd {
		margin-bottom: 16rpx;
		white-space: pre-wrap;
		font-size: 36rpx;
		font-weight: bold;
		color: #333333;
		line-height: 48rpx;
	}

	.boxlbd {
		font-size: 30rpx;
		font-weight: 400;
		color: #333333;
		line-height: 46rpx;
		white-space: pre-wrap;
	}

	.boxr {
		width: 96rpx;
		display: flex;
		align-items: center;
		position: relative;
	}

	.boxr::before {
		width: 2rpx;
		height: 96rpx;
		background: #e3e3e3;
		content: "";
		position: relative;
		left: 0;
		z-index: 99;
	}

	.boxrimg {
		width: 64rpx;
		height: 64rpx;
		margin: 0 auto;
	}
</style>