<template>
	<view>
		<page-head :title="title"></page-head>
		<view class="c-padding-wrap c-common-mt">
			<view class="c-title">
				<c-icon size="16" type="info"></c-icon>说明 : </view>
			<view class="c-helllo-text">
				<view>在App端可在pages.json里通过 style -> app-plus -> tags 配置，暂不支持动态改变tags的样式；常用于App首页顶部导航显示产品Logo</view>
			</view>
		</view>
	</view>
</template>
<script>
	import uniIcon from '@/components/c-icon/c-icon.vue'
	export default {
		data() {
			return {
				title: 'nav-image'
			}
		},
		components:{
			uniIcon
		}
	}
</script>

<style>
	
</style>
