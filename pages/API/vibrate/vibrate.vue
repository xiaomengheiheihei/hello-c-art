<template>
	<view>
		<page-head :title="title"></page-head>
		<view class="c-padding-wrap">
			<button class="c-button" type="primary" @click="longshock">长震动</button>
			<button class="c-button" @click="shortshock">短震动</button>

			<view class="c-tips">
				<view>Tips</view>
				<view class="c-tips-text">iOS上只有长震动，没有短震动</view>
				<view class="c-tips-text">iOS上需要手机设置“打开响铃时震动”或“静音时震动”，否则无法震动</view>
			</view>
		</view>
	</view>
</template>
<script>
export default {
	data() {
		return {
			title: 'vibrateLong/vibrateShort'
		};
	},
	onLoad() {},
	methods: {
		longshock() {
			c.vibrateLong({
				success: function() {
					console.log('success');
				}
			});
		},
		shortshock() {
			c.vibrateShort({
				success: function() {
					console.log('success');
				}
			});
		}
	}
};
</script>

<style>
.c-padding-wrap {
	margin-top: 50upx 0;
}
.c-button {
	margin: 30upx 0;
}
.c-tips {
	color: #666;
	font-size: 30upx;
}
.c-tips-text {
	margin-top: 15upx;
	line-height: 1.2;
	font-size: 24upx;
}
</style>
