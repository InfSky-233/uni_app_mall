<template>
	<view>
		<view class="news_item" v-for="(item, index) in newslist" :key="index">
			<image :src="item.img_url"></image>
			<view class="right">
				<view class="title">
					{{item.title}}
				</view>
				<view class="abstract">
					{{item.zhaiyao}}
				</view>
				<view class="title_bottom">
					<text>发布时间：{{item.add_time | dataFilter}}</text>
					<text>浏览：{{item.click}}</text>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		props: ['newslist'],
		filters: {
			dataFilter(date) {
				const nDate = new Date(date)
				const year = nDate.getFullYear()
				const month = nDate.getMonth() + 1
				const nmonth = month.toString().padStart(2, 0)
				const day = nDate.getDate().toString().padStart(2, 0)
				return year + '-' + nmonth + '-' + day
			}
		},
		
	}
</script>

<style lang="scss">
	.news_item {
		display: flex;
		padding: 20rpx;
		border-bottom: 2rpx solid #eee;

		image {
			max-width: 200rpx;
			max-height: 200rpx;
			border-radius: 6rpx;
			margin-right: 20rpx;
		}

		.right {
			display: flex;
			flex-direction: column;
			justify-content: space-between;

			.title {
				font-size: 30rpx;
				font-weight: bold;
			}

			.abstract {
				font-size: 26rpx;
			}

			.title_bottom {
				color: #949494;
				font-size: 24rpx;
			}

			.title_bottom>text:nth-child(2) {
				margin-left: 50rpx;
			}
		}
	}
</style>
