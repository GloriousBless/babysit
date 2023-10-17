# liu-easy-map 适用于uni-app项目的map地图组件
### 本组件目前兼容微信小程序、H5
### 本组件是超级简单好用map地图，支持标记点、画区域、标记点详情弹层、导航等(走过路过不要错过)
### 如使用过程中有问题或有一些好的建议，欢迎qq联系：2364518038

### 注意事项
### 由于组件内使用getLocation官方api获取当前定位，上线前需在公众平台开通并在manifest.json中配置
### 因组件根本为内置map组件，组件包含多个属性均与官方文档差异说明一致，建议使用者先大概阅读官方文档

### 使用示例
``` 
<template>
	<view class="page-main">
		<liu-easy-map ref="liuEasyMap" :centerLat="'36.05709'" :centerLng="'103.82538'" :scale="14"
			:markerData="markerData" :polygons="polygons" @clickMarker="markerClick"></liu-easy-map>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				markerData: [{
					id: 1,
					name: '兰州市政府', //标记点展示名字
					address: '甘肃省兰州市城关区人民政府',
					latitude: '36.05989', //标记点纬度
					longitude: '103.83502', //标记点经度
					markerUrl: 'https://img0.baidu.com/it/u=550544800,2229099292&fm=253&fmt=auto&app=138&f=JPEG?w=500&h=500', //标记点图标地址
					iconWidth: 32, //标记点图标宽度
					iconHeight: 32, //标记点图标高度
					calloutColor: '#ffffff', //气泡窗口 文本颜色
					calloutFontSize: 14, //气泡窗口 文本大小
					calloutBorderRadius: 6, //气泡窗口 边框圆角
					calloutPadding: 8, //气泡窗口 文本边缘留白
					calloutBgColor: '#0B6CFF', //气泡窗口 背景颜色
					calloutDisplay: 'ALWAYS', //气泡窗口 展示类型 默认常显 'ALWAYS' 常显 'BYCLICK' 点击显示
				}, {
					id: 2,
					name: '测试地址', //标记点展示名字
					address: '测试地址详细地址测试地址详细地址测试地址详细地址测试地址详细地址',
					latitude: "36.05064",
					longitude: "103.82538"
				}],
				//展示区域点位信息
				polygons: [{
					points: [{
						latitude: "36.06637",
						longitude: "103.82471"
					}, {
						latitude: "36.06255",
						longitude: "103.82321"
					}, {
						latitude: "36.06234",
						longitude: "103.81928"
					}, {
						latitude: "36.06036",
						longitude: "103.82175"
					}, {
						latitude: "36.05653",
						longitude: "103.82152"
					}, {
						latitude: "36.05953",
						longitude: "103.82476"
					}, {
						latitude: "36.05690",
						longitude: "103.82785"
					}, {
						latitude: "36.06023",
						longitude: "103.82747"
					}, {
						latitude: "36.06243",
						longitude: "103.83014"
					}, {
						latitude: "36.06245",
						longitude: "103.82616"
					}],
					strokeWidth: 2,
					strokeColor: "#FF000060",
					fillColor: "#FF000090"
				}]
			}
		},
		methods: {
			//点击标记点
			markerClick(item) {
				//拿到当前点击的标记点，数据对象，写自己的业务逻辑
				//例如 展示详情弹层、导航等
				console.log(item)
			}
		}
	}
</script>

<style lang="scss">
	.page-main {
		width: 100%;
		height: 100vh;
	}
</style>
```

### 属性说明
| 名称                         | 类型            | 默认值                 | 描述            |
| ----------------------------|--------------- | ---------------------- | ---------------|
| centerLat                   | String         | 当前定位纬度             | 地图展示中心点纬度
| centerLng                 	| String         | 当前定位经度             | 地图展示中心点经度
| markerData                  | Array          | []                     | 标记点数据
| polygons		                | Array          | []                     | 多边形数据
| markerIconWidth             | Number         | 22                     | 标记点图标宽度
| markerIconHeight            | Number         | 32                     | 标记点图标高度
| markerIconUrl               | String         | ''                     | 标记点图标路径
| scale                      	| Number         | 16                     | 缩放级别 取值范围为3-20
| isShowCompass               | Boolean        | false                  | 是否显示指南针
| isEnableZoom                | Boolean        | true                   | 是否支持缩放
| isEnableScroll              | Boolean        | true                   | 是否支持拖动
| isEnableRotate              | Boolean        | false                  | 是否支持旋转
| @clickMarker                | Function        |                       | 点击标记点回调事件
| @clickMap                   | Function        |                       | 点击地图(微信小程序2.9支持)
