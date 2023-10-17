<template>
	<view>
		<view class="m-search-container">
			<view class="left">
			  <slot name="left"></slot>
			</view>
		  <view class="input-container" :style="{borderColor: input_border_color, backgroundColor: input_bg_color}">    
			<input :focus="focus" class="search-input" type="text" :value="inputValue"  @input="input" @confirm="search"/>  
			<view class="right">
				<slot name="right"></slot>
			</view>
		  </view>
		  
		</view>
	</view>
</template>

<script>
	export default {
		name:"MySearch",
		props:{
			msg: {
				type: String,
				default: "请输入"
			},
			input_border_color: {
				type: String,
				default: "rgba(100,100,100,0)"
			},
			input_bg_color: {
				type: String,
				default: "rgba(100,100,100,0.08)"
			},
			focus: {
				type: Boolean,
				default: false
			},
			inputValue: {
				type: String,
				default: ''
			}
		},
		data() {
			return {
				bgColor: 'red',
			};
		},
		methods: {
			input(event) {
				this.$emit('input', event)
			},
			search() {
				this.$emit('search')
			}
		}
	}
</script>

<style lang="scss">
/* components/component-tag-name.wxss */
.m-search-container {
  display: flex;
	flex-wrap: nowrap;
  height: 60rpx;
  line-height: 60rpx;
  margin: 50rpx;
	margin-bottom: 0;
}

.input-container {
	flex-grow: 1;
	border-radius: 15rpx;
	display: flex;
	align-items: center;
	border-width: 4rpx;
	margin-right: 20rpx;

	input {
		margin-left: 20rpx;
		width: 88%;
	}
}

.left {
	padding: 0 10rpx;
}

.right {
	
	white-space: nowrap;
}


</style>
