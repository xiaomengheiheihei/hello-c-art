<template>
	<view class="page">
		<view class="example">
			<view class="example-title">有底色</view>
			<view style="background:#FFF; padding:20upx;">
				<c-badge text="1" />
				<c-badge text="2" type="primary" />
				<c-badge text="34" type="success" />
				<c-badge text="45" type="warning" />
				<c-badge text="123" type="error" />
			</view>
			<view class="example-title">无底色</view>
			<view style="background:#FFF; padding:20upx;">
				<c-badge :inverted="true" text="1" />
				<c-badge :inverted="true" text="2" type="primary" />
				<c-badge :inverted="true" text="34" type="success" />
				<c-badge :inverted="true" text="45" type="warning" />
				<c-badge :inverted="true" text="123" type="error" />
			</view>
			<view class="example-title">迷你</view>
			<view style="background:#FFF; padding:20upx;">
				<c-badge text="1" size="small" />
				<c-badge text="2" type="primary" size="small" />
				<c-badge text="34" type="success" size="small" />
				<c-badge text="45" type="warning" size="small" />
				<c-badge text="123" type="error" size="small" />
			</view>
		</view>
	</view>
</template>

<script>
	import uniBadge from '@/components/c-badge/c-badge.vue'

	export default {
		components: {
			uniBadge
		},
		data() {
			return {}
		}
	}
</script>

<style>
	page {
		display: flex;
		flex-direction: column;
		box-sizing: border-box;
		background-color: #fff
	}

	view {
		font-size: 28upx;
		line-height: inherit
	}

	.example {
		padding: 0 30upx 30upx
	}

	.example-title {
		font-size: 32upx;
		line-height: 32upx;
		color: #777;
		margin: 40upx 25upx;
		position: relative
	}

	.example .example-title {
		margin: 40upx 0
	}

	.example-body {
		padding: 0 40upx
	}

	.c-badge {
		margin: 20upx;
	}
</style>