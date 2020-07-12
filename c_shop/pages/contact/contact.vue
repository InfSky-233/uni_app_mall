<template>
	<view>
		<image src="../../static/about.png"></image>
		<view class="top">关于我们</view>
		<view class="com tel" @click="callphone">
			联系电话：400 123 1234
		</view>
		<view class="com addrs">
			公司地址：重庆市渝中区接圣街8号（来福士）
		</view>
		<map :latitude="latitude" :longitude="longitude" scale='17' :markers="covers"></map>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				latitude: 29.564667,
				longitude: 106.586952,
				covers: [{
					latitude: 29.564667,
					longitude: 106.586952
				}]
			}
		},
		methods: {
			callphone() {
				uni.makePhoneCall({
					phoneNumber: '4001231234'
				});
			}
		}
	}
</script>

<style lang="scss">
	image {
		width: 100%;
		height: 300rpx;
		filter: blur(1rpx);
	}

	.top {
		color: #ffffff;
		font-size: 50rpx;
		font-weight: bold;
		letter-spacing: 16rpx;
		position: absolute;
		top: 150rpx;
		left: 50%;
		transform: translate(-50%, -50%);
	}

	.com {
		font-size: 34rpx;
		margin: 20rpx;
		padding-bottom: 20rpx;
	}

	.tel {
		border-bottom: 2rpx solid #eee;
	}

	map {
		width: 100%;
		height: 900rpx;
	}
</style>
