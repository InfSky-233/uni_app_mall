<template>
	<view class="home">
		<!-- 轮播图区域 -->
		<swiper :indicator-dots="true" :autoplay="true" circular :interval="3000" :duration="1000">
			<swiper-item v-for="item in swipers" :key="item.id">
				<image :src="item.img"></image>
			</swiper-item>
		</swiper>
		<!-- 导航区域 -->
		<view class="nav">
			<view class="nav_item" v-for="(item, index) in navs" :key="index" @click="toNav(item.path)">
				<view :class="item.icon"></view>
				<text>{{item.title}}</text>
			</view>
		</view>
		<!-- 推荐商品区域 -->
		<view class="hot_goods">
			<view class="title">推荐商品</view>
			<goods_list :goods="goods" :showtips="showtips"></goods_list>
		</view>
	</view>
</template>

<script>
	import goodsList from '../../components/goods/goods_list.vue'
	export default {
		data() {
			return {
				swipers: [],
				goods: [],
				goodspage: 1,
				showtips: false,
				navs: [
					{
						icon: 'iconfont icon-ziyuan',
						title: '同城超市',
						path: '/pages/goods/goods'
					},
					{
						icon: 'iconfont icon-guanyuwomen',
						title: '联系我们',
						path: '/pages/contact/contact'
					},
					{
						icon: 'iconfont icon-tupian',
						title: '社区图片',
						path: '/pages/picas/picas'
					},
					{
						icon: 'iconfont icon-shipin',
						title: '学习视频',
						path: '/pages/videos/videos'
					}
				]
			}
		},
		components: {
			'goods_list': goodsList
		},
		onLoad() {
			this.getSwiper(),
				this.getGoods()
		},
		onReachBottom() {
			this.getGoods()
		},
		methods: {
			// 获取轮播图数据
			async getSwiper() {
				const res = await this.$myRequest({
					url: '/api/getlunbo'
				})
				this.swipers = res.data.message
			},
			// 获取商品列表数据
			async getGoods() {
				const res = await this.$myRequest({
					url: '/api/getgoods?pageindex=' + this.goodspage
				})
				if (res.data.message.length == 0) {
					this.showtips = true
				} else {
					this.goodspage += 1
					this.goods.push(...res.data.message)
				}
			},
			// 导航栏跳转
			toNav(path) {
				uni.navigateTo({
				    url: path
				});
			}
		}
	}
</script>

<style lang="scss">
	.home {
		swiper {
			width: 100%;
			height: 380rpx;

			image {
				width: 100%;
				height: 100%;
			}
		}

		.nav {
			display: flex;

			.nav_item {
				flex: 1;
				text-align: center;

				.iconfont {
					width: 90rpx;
					height: 90rpx;
					font-size: 40rpx;
					background: $shop-color;
					border-radius: 50%;
					line-height: 90rpx;
					margin: 14rpx auto;
					color: #fff;
				}

				.icon-tupian {
					font-size: 35rpx;
				}

				text {
					font-size: 26rpx;
				}
			}
		}

		.hot_goods {
			background: #eee;
			overflow: hidden;
			margin-top: 10rpx;

			.title {
				height: 70rpx;
				line-height: 70rpx;
				color: $shop-color;
				text-align: center;
				font-size: 36rpx;
				font-weight: bold;
				letter-spacing: 40rpx;
				background: #fff;
				margin-top: 7rpx;
				margin-bottom: -8rpx;
			}
		}
	}
</style>
