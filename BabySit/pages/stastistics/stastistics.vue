<template>
	<view class="stastics">
		<scroll-view scroll-y>
			<view class="temperature">
				<text class="text">每日体温记录</text>
				<view class="charts-box">
				    <qiun-data-charts 
				      type="bar"
				      :opts="opts"
				      :chartData="chartData"
				    />
				  </view>
			</view>
			
			<out-tempra></out-tempra>
			<month-weight></month-weight>
			
			<view class="weight-incre" @touchstart="changeColor1"  @touchend="changeColor2" :class=" act_color1==true ? 'active':''">
				<image src="../../static/stastics/cheng.png" class="img"></image>
				<text class="text">宝宝该月比上月增重0.5kg</text>
			</view>
			<view class="conclusion" @touchstart="changeColor3"  @touchend="changeColor4" :class=" act_color2==true ? 'active':''">
				<image src="../../static/stastics/conclusion.png" class="img"></image>
				<text class="text">婴儿最近体温正常，室外环境温度较高，注意防晒，体重方面注意饮食</text>
			</view>
			<view style="height: 30rpx;"></view>
		</scroll-view>
	</view>
</template>

<script>
export default {
  data() {
    return {
      chartData: {},
      //这里的 opts 是图表类型 type="bar" 的全部配置参数，您可以将此配置复制到 config-ucharts.js 文件中下标为 ['bar'] 的节点中来覆盖全局默认参数。实际应用过程中 opts 只需传入与全局默认参数中不一致的【某一个属性】即可实现同类型的图表显示不同的样式，达到页面简洁的需求。
      opts: {
      },
	  act_color1:false,
	  act_color2:false

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
            categories: ["4月17日","4月16日","4月15日","4月14日","4月13日","4月12日"],
            series: [
              {
                name: "宝宝体温℃",
                color: "#d5a4cf",
                textSize: 9,
                data: [36.9,36.8,37.5,37.1,37.4,36.9]
              }
            ]
          };
        this.chartData = JSON.parse(JSON.stringify(res));
      }, 500);
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
					}
	
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
	.weight-incre{
		background-color: #ffffff;
		border-radius: 15rpx;
		box-shadow: 0 0  15rpx 5rpx #d5a4cf;
		margin-top: 30rpx;
		margin-left: 30rpx;
		width: 93%;
		height: 180rpx;
		text-align: center;
		display: flex;
		.img{
			width: 150rpx;
			height: 150rpx;
			margin-top: 20rpx;
		}
		.text{
			margin-left: 30rpx;
			line-height: 180rpx;
			font-size: 35rpx;
			color: #a396d5;
			font-weight: bold;
			font-family: "SimSun";
		}
	}
	.conclusion{
		background-color: #ffffff;
		border-radius: 15rpx;
		box-shadow: 0 0  15rpx 5rpx #d5a4cf;
		margin-top: 30rpx;
		margin-left: 30rpx;
		width: 93%;
		height: 180rpx;
		text-align: center;
		display: flex;
		.img{
			width: 120rpx;
			height: 120rpx;
			margin: 30rpx 0 0 20rpx;
		}
		.text{
			width: 80%;
			padding-top: 50rpx;
			padding-right: 5rpx;
			margin-left: 15rpx;
			font-size: 35rpx;
			color: #a396d5;
			font-weight: bold;
			font-family: "SimSun";
		}
	}
	.active{
		background-color: #EAEAEA;
	}
</style>
