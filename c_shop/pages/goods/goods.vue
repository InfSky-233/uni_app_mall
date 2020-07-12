<template>
	<view class="wrap">
		<goods_list :goods="goods" :showtips="showtips"></goods_list>
	</view>
</template>

<script>
	import goodsList from '../../components/goods/goods_list.vue'
	export default {
		data() {
			return {
				goods: [],
				goodspage: 1,
				showtips: false
			}
		},
		components: {
			'goods_list': goodsList
		},
		onLoad() {
			this.getGoods()
		},
		onReachBottom() {
			this.getGoods()
		},
		onPullDownRefresh() {
			this.goodspage = 1
			this.showtips = false
			this.goods = []
			setTimeout(() => {
				this.getGoods()
				uni.stopPullDownRefresh()
			}, 500);
		},
		methods: {
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
			}
		}
	}
</script>

<style lang="scss">
	.wrap {
		background: #eee;
	}
</style>
