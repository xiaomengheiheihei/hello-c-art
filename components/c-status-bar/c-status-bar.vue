<template>
	<view :style="{ height: statusBarHeight }" class="c-status-bar">
		<slot />
	</view>
</template>

<script>
	var statusBarHeight = c.getSystemInfoSync().statusBarHeight + 'px'
	export default {
		name: 'UniStatusBar',
		data() {
			return {
				statusBarHeight: statusBarHeight
			}
		}
	}
</script>

<style>
	.c-status-bar {
		display: block;
		width: 100%;
		height: 20px;
		height: var(--status-bar-height);
	}
</style>