<template>
	<view>
		<page-head :title="title"></page-head>
		<view class="c-padding-wrap c-common-mt">
			<view class="c-title">扫码结果：</view>
			<view class="c-list" v-if="result">
				<view class="c-cell">
					<view class="scan-result">
						{{result}}
					</view>
				</view>
			</view>
			<view class="c-btn-v">
				<button type="primary" @click="scan">扫一扫</button>
			</view>
		</view>
	</view>
</template>
<script>
	export default {
		data() {
			return {
				title: 'scanCode',
				result: ''
			}
		},
		methods: {
			scan: function() {
				c.scanCode({
					success: (res) => {
						this.result = res.result
					}
				});
			}
		}
	}
</script>

<style>
	.scan-result {
		min-height: 50upx;
		line-height: 50upx;
	}
</style>
