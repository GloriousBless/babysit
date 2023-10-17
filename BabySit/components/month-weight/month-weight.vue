<template>
	<view class="temperature">
		<text class="text">宝宝体重变化</text>
		  <view class="charts-box">
			<qiun-data-charts 
			  type="area"
			  :opts="opts"
			  :chartData="chartData"
			/>
		  </view>
	</view>
</template>

<script>
export default {
	name:"month-weight",
  data() {
    return {
      chartData: {},
      //这里的 opts 是图表类型 type="area" 的全部配置参数，您可以将此配置复制到 config-ucharts.js 文件中下标为 ['area'] 的节点中来覆盖全局默认参数。实际应用过程中 opts 只需传入与全局默认参数中不一致的【某一个属性】即可实现同类型的图表显示不同的样式，达到页面简洁的需求。
      opts: {
        timing: "easeOut",
        duration: 1000,
        rotate: false,
        rotateLock: false,
        color: ["#1890FF","#91CB74","#FAC858","#EE6666","#73C0DE","#3CA272","#FC8452","#9A60B4","#ea7ccc"],
        padding: [15,15,0,15],
        fontSize: 10,
        fontColor: "#666666",
        dataLabel: true,
        dataPointShape: true,
        dataPointShapeType: "solid",
        touchMoveLimit: 60,
        enableScroll: false,
        enableMarkLine: false,
        legend: {
          show: true,
          position: "bottom",
          float: "center",
          padding: 5,
          margin: 5,
          backgroundColor: "rgba(0,0,0,0)",
          borderColor: "rgba(0,0,0,0)",
          borderWidth: 0,
          fontSize: 10,
          fontColor: "#666666",
          lineHeight: 11,
          hiddenColor: "#CECECE",
          itemGap: 10
        },
        xAxis: {
          disableGrid: true,
          disabled: false,
          axisLine: true,
          axisLineColor: "#CCCCCC",
          calibration: false,
          fontColor: "#666666",
          fontSize: 10,
          lineHeight: 20,
          marginTop: 0,
          rotateLabel: false,
          rotateAngle: 45,
          itemCount: 5,
          boundaryGap: "center",
          splitNumber: 5,
          gridColor: "#CCCCCC",
          gridType: "solid",
          dashLength: 4,
          gridEval: 1,
          scrollShow: false,
          scrollAlign: "left",
          scrollColor: "#A6A6A6",
          scrollBackgroundColor: "#EFEBEF",
          title: "",
          titleFontSize: 13,
          titleOffsetY: 0,
          titleOffsetX: 0,
          titleFontColor: "#666666",
          format: ""
        },
        yAxis: {
          gridType: "dash",
          dashLength: 2,
          disabled: false,
          disableGrid: false,
          splitNumber: 2,
          gridColor: "#CCCCCC",
          padding: 10,
          showTitle: false,
          data: []
        },
        extra: {
          area: {
            type: "straight",
            opacity: 0.2,
            addLine: true,
            width: 2,
            gradient: false,
            activeType: "hollow"
          },
          tooltip: {
            showBox: true,
            showArrow: true,
            showCategory: false,
            borderWidth: 0,
            borderRadius: 0,
            borderColor: "#000000",
            borderOpacity: 0.7,
            bgColor: "#000000",
            bgOpacity: 0.7,
            gridType: "solid",
            dashLength: 4,
            gridColor: "#CCCCCC",
            boxPadding: 3,
            fontSize: 13,
            lineHeight: 20,
            fontColor: "#FFFFFF",
            legendShow: true,
            legendShape: "auto",
            splitLine: true,
            horizentalLine: false,
            xAxisLabel: false,
            yAxisLabel: false,
            labelBgColor: "#FFFFFF",
            labelBgOpacity: 0.7,
            labelFontColor: "#666666"
          },
          markLine: {
            type: "solid",
            dashLength: 4,
            data: []
          }
        }
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
            categories: ["1月","2月","3月","4月","5月","6月","7月"],
            series: [
              {
                name: "宝宝体重变化 kg",
                color: "#79BEDB",
                data: [9.6,9.5,9.9,10.1,10.3,10.4,10.7]
              }
            ]
          };
        this.chartData = JSON.parse(JSON.stringify(res));
      }, 500);
    },
  }
};
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