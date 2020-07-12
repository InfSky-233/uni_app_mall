<template>
	<view class="pics">
		<scroll-view class="left" scroll-y="true">
			<view class="imgitem" :class="active===index ? 'active' : ''" v-for="(item, index) in imgcategory" :key="index"
			 @click="handleItem(index, item.id)">{{item.title}}</view>
		</scroll-view>
		<scroll-view class="right" scroll-y="true">
			<view class="tips" v-if="imgdata.length === 0">
				该分类暂无图片
			</view>
			<view class="img" v-else v-for="(item, index) in imgdata" :key="index">
				<image :src="item.img_url" lazy-load="true" @click="previewImage(imgarr, index)"></image>
				<view class="title">
					{{item.title}}
				</view>
			</view>
		</scroll-view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				imgcategory: [],
				active: 0,
				imgdata: [0],
				imgarr: []
			}
		},
		onLoad() {
			this.getImgCategory()
			this.getImgInfo(14)
		},
		methods: {
			// 获取图片分类
			async getImgCategory() {
				const res = await this.$myRequest({
					url: '/api/getimgcategory'
				})
				this.imgcategory = res.data.message
			},
			// 获取图片信息
			async getImgInfo(id) {
				const res = await this.$myRequest({
					url: '/api/getimages/' + id
				})
				this.imgdata = res.data.message
				this.imgarr = res.data.message.map(item => {
					return item.img_url
				})
			},
			handleItem(index, id) {
				this.active = index
				this.getImgInfo(id)

			},
			// 预览图片
			previewImage(url, index) {
				uni.previewImage({
					urls: url,
					current: index,
					indicator: "default",
					loop: true
				})
			}
		}
	}
</script>

<style lang="scss">
	page {
		height: 100%;

		.pics {
			height: 100%;
			display: flex;
			flex-direction: row;

			.left {
				width: 210rpx;
				height: 100%;
				border-right: 2rpx solid #eee;

				.imgitem {
					width: 100%;
					height: 120rpx;
					font-size: 34rpx;
					text-align: center;
					line-height: 120rpx;
					border-bottom: 2rpx solid #eee;
				}

				.active {
					color: #fff;
					background: $shop-color;
				}
			}

			.right {
				width: 500rpx;
				height: 100%;
				margin: 0 auto;

				.tips {
					font-size: 30rpx;
					text-align: center;
					margin-top: 100rpx;
				}

				.img {
					margin: 20rpx auto;
					padding-bottom: 10rpx;
					border-bottom: 2rpx solid #eee;

					image {
						width: 100%;
						border-radius: 7rpx;
					}

					.title {
						font-size: 30rpx;
					}
				}
			}
		}
	}
</style>
