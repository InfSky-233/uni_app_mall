<template>
	<view>
		<newslist :newslist="newslist"></newslist>
	</view>
</template>

<script>
	import newsList from '../../components/newslist/newslist'
	export default {
		components: {
			'newslist': newsList
		},
		data() {
			return {
				newslist: []
			}
		},
		onLoad() {
			this.getNews()
		},
		methods: {
			async getNews() {
				const res = await this.$myRequest({
					url: '/api/getnewslist'
				})
				this.newslist = res.data.message
			}
		}
	}
</script>

<style lang="scss">

</style>
