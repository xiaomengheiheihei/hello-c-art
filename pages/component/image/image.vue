<template>
	<view>
		<page-head :title="title"></page-head>
		<view class="c-padding-wrap c-common-mt">
			<view class="c-title">
				示例1 <text>\n本地图片</text>
			</view>
			<view class="c-center" style="background:#FFFFFF; font-size:0;">
				<!-- #ifdef MP-ALIPAY -->
				<image class="image" mode="widthFix" src="../../../static/c.png" />
				<!-- #endif -->
				<!-- #ifndef MP-ALIPAY -->
				<image class="image" mode="widthFix" src="../../../static/c.png" />
				<!-- #endif -->
			</view>
			<view class="c-title c-common-mt">
				示例2 <text>\n网络图片</text>
			</view>
			<view class="c-center" style="background:#FFFFFF; font-size:0;">
				<image class="image" mode="widthFix" src="https://img-cdn-qiniu.dcloud.net.cn/uniapp/images/uni@2x.png" />
			</view>
		</view>
	</view>
</template>
<script>
	export default {
		data() {
			return {
				title: 'image'
			}
		}
	}
</script>
<style>
	.image {
		margin:40upx 0;
		width: 200upx;
	}
</style>
