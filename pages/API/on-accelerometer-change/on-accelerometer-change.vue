<template>
	<view>
		<page-head :title="title"></page-head>
		<view class="c-padding-wrap c-common-mt">
			<!-- #ifdef APP-PLUS -->
			<view class="c-btn-v">
				<button class="shake" @tap="shake">摇一摇</button>
			</view>
			<!-- #endif -->
			<view class="c-btn-v">
				<button type="primary" @tap="watchAcce">监听设备的加速度变化</button>
				<button type="primary" @tap="stopAcce">停止监听设备的加速度变化</button>
			</view>
			<view class="c-textarea c-common-mt">
				<textarea :value="value" auto-height="true"/>
			</view>
		</view>
	</view>
</template>
<script>

	export default {
		data() {
			return {
				title: 'onAccelerometerChange',
				value: ''
			}
		},
		onUnload() {
			c.stopAccelerometer();
		},
		methods: {
			//#ifdef APP-PLUS
			shake() {
				c.navigateTo({
					url: '/platforms/app-plus/shake/shake'
				})
			},
			//#endif
			watchAcce() {
				c.onAccelerometerChange((res) => {
					this.value = "监听设备的加速度变化:\n" + "X轴：" + res.x.toFixed(2) + "\nY轴：" + res.y.toFixed(2) +
						"\nZ轴：" + res.z.toFixed(2);
				})
			},
			stopAcce() {
				c.stopAccelerometer()
			}
		}
	}
</script>

<style>
	.shake {
		background-color: #FFCC33;
		color: #ffffff;
		margin-bottom: 50upx;
	}
</style>
