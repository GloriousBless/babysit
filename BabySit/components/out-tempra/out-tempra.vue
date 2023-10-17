<template>
	<view>
		<view class="temperature">
			<text class="text">室外温度</text>
			<view class="charts-box">
			    <qiun-data-charts 
			      type="line"
			      :opts="opts"
			      :chartData="chartData"
			    />
			  </view>
		</view>
	</view>
</template>

<script>
	export default {
		name:"out-tempra",
		data() {
			return {
				chartData: {},
				      //这里的 opts 是图表类型 type="line" 的全部配置参数，您可以将此配置复制到 config-ucharts.js 文件中下标为 ['line'] 的节点中来覆盖全局默认参数。实际应用过程中 opts 只需传入与全局默认参数中不一致的【某一个属性】即可实现同类型的图表显示不同的样式，达到页面简洁的需求。
				      opts: {
				      }
			};
		},
		onReady() {
		    this.getServerData();
		  },
		  methods: {
		    getServerData() {
		      //模拟从服务器获取数据时的延时
		      setTimeout(() => {
		        //模拟服务器返回数据，如果数据格式和标准格式不同，需自行按下面的格式拼接
		        let res = {
		            categories: ["0:00","2:00","4:00","6:00","8:00","10:00","12:00","14:00","16:00","18:00","20:00","22:00"],
		            series: [
		              {
		                name: "室外温度℃",
		                data: [24,23.5,24,24,25,29,30,33,31,29,27,25,24]
		              }
		            ]
		          };
		        this.chartData = JSON.parse(JSON.stringify(res));
		      }, 500);
		    },
		  }
	}
</script>

<style lang="scss" scoped>
	.temperature{
		background-color: #ffffff;
		border-radius: 15rpx;
		box-shadow: 0 0  20rpx 5rpx #d5a4cf;
		margin-top: 30rpx;
		margin-left: 30rpx;
		width: 93%;
		height: 500rpx;
		text-align: center;
		.text{		
			padding-top: 5rpx;
			font-size: 35rpx;
			font-weight: bolder;
		}
		/* 请根据实际需求修改父元素尺寸，组件自动识别宽高 */
		  .charts-box {
		    width: 100%;
		    height: 450rpx;
		  }
	}
</style>