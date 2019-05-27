<template>
	<view class="page">
		<page-head :title="title"></page-head>
		<view class="c-padding-wrap">
			<view class="c-helllo-text">
				本页标题栏是c-app的默认配置，开发者可在pages.json里配置文字内容及标题颜色，也可通过api接口将其改变。
			</view>
			<view class="c-btn-v">
				<button type="default" @click="setText">改变标题栏文字</button>
				<!-- #ifndef MP-TOUTIAO -->
				<button type="primary" @click="setBg">改变标题栏颜色</button>
				<!-- #endif -->
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: 'nav-default',
				hasSetText:false,
				hasSetBg:false
			}
		},
		methods: {
			setText() {
				this.hasSetText = !this.hasSetText;
				c.setNavigationBarTitle({
					title: this.hasSetText ? "Hello c-app" : "默认导航栏"
				})
			},
			setBg() {
				this.hasSetBg = !this.hasSetBg;
				c.setNavigationBarColor({
					frontColor: this.hasSetBg ? "#ffffff" : "#000000",
					backgroundColor: this.hasSetBg ? "#007AFF" : "#F8F8F8"
				})
			}
		}
	}
</script>

<style>
</style>
