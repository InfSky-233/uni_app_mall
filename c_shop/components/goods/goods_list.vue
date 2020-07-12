<template>
	<view>
		<view class="goods_list">
			<view class="goods_item" v-for="(item, index) in goods" :key="index">
				<image :src="item.img_url" lazy-load="true"></image>
				<text class="price">￥{{item.market_price}}</text>
				<text class="line_price">￥{{item.sell_price}}</text>
				<view class="pr_name">{{item.title}}</view>
			</view>
		</view>
		<view class="bottom_tips" v-if="showtips">没有更多了哦~</view>
	</view>
</template>

<script>
	export default {
		props: ['goods', 'showtips'],
	}
</script>

<style lang="scss">
	.goods_list {
		display: flex;
		flex-wrap: wrap;
		justify-content: space-around;

		.goods_item {
			width: 48%;
			height: 540rpx;
			background: #fff;
			margin-top: 14rpx;
			padding: 24rpx;
			box-sizing: border-box;

			image {
				width: 100%;
				height: 312rpx;
				margin-bottom: 10rpx;
				box-sizing: border-box;
			}

			.price {
				color: $shop-color;
				font-size: 32rpx;
			}

			.line_price {
				color: #a1a1a1;
				font-size: 26rpx;
				margin-left: 20rpx;
				text-decoration: line-through;
			}

			.pr_name {
				font-size: 28rpx;
				margin-top: 10rpx;
			}
		}
	}

	.bottom_tips {
		height: 60rpx;
		color: #8f8f8f;
		margin: 10rpx;
		text-align: center;
		line-height: 60rpx;
		font-size: 28rpx;
	}
</style>
