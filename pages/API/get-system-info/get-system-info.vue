<template>
	<view>
		<page-head :title="title"></page-head>
		<view class="c-common-mt">
			<view class="c-list">
				<view class="c-list-cell">
					<view class="c-pd">
						<view class="c-label" style="width:180px;">手机型号</view>
					</view>
					<view class="c-list-cell-db">
						<input class="c-input" type="text" :disabled="true" placeholder="未获取" :value="systemInfo.model"></input>
					</view>
				</view>
				<view class="c-list-cell">
					<view class="c-pd">
						<view class="c-label" style="width:180px;">客户端平台</view>
					</view>
					<view class="c-list-cell-db">
						<input class="c-input" type="text" :disabled="true" placeholder="未获取" :value="systemInfo.platform"></input>
					</view>
				</view>
				<view class="c-list-cell">
					<view class="c-pd">
						<view class="c-label" style="width:180px;">操作系统版本</view>
					</view>
					<view class="c-list-cell-db">
						<input class="c-input" type="text" :disabled="true" placeholder="未获取" :value="systemInfo.system"></input>
					</view>
				</view>
				<view class="c-list-cell">
					<view class="c-pd">
						<view class="c-label" style="width:180px;">语言</view>
					</view>
					<view class="c-list-cell-db">
						<input class="c-input" type="text" :disabled="true" placeholder="未获取" :value="systemInfo.language"></input>
					</view>
				</view>
				<view class="c-list-cell">
					<view class="c-pd">
						<view class="c-label" style="width:180px;">版本</view>
					</view>
					<view class="c-list-cell-db">
						<input class="c-input" type="text" :disabled="true" placeholder="未获取" :value="systemInfo.version"></input>
					</view>
				</view>
				<view class="c-list-cell">
					<view class="c-pd">
						<view class="c-label" style="width:180px;">屏幕宽度</view>
					</view>
					<view class="c-list-cell-db">
						<input class="c-input" type="text" :disabled="true" placeholder="未获取" :value="systemInfo.screenWidth"></input>
					</view>
				</view>
				<view class="c-list-cell">
					<view class="c-pd">
						<view class="c-label" style="width:180px;">屏幕高度</view>
					</view>
					<view class="c-list-cell-db">
						<input class="c-input" type="text" :disabled="true" placeholder="未获取" :value="systemInfo.screenHeight"></input>
					</view>
				</view>
				<view class="c-list-cell">
					<view class="c-pd">
						<view class="c-label" style="width:180px;">可使用窗口高度</view>
					</view>
					<view class="c-list-cell-db">
						<input class="c-input" type="text" :disabled="true" placeholder="未获取" :value="systemInfo.windowHeight"></input>
					</view>
				</view>
				<view class="c-list-cell">
					<view class="c-pd">
						<view class="c-label" style="width:180px;">可使用窗口的顶部位置</view>
					</view>
					<view class="c-list-cell-db">
						<input class="c-input" type="text" :disabled="true" placeholder="未获取" :value="systemInfo.windowTop"></input>
					</view>
				</view>
				<view class="c-list-cell">
					<view class="c-pd">
						<view class="c-label" style="width:180px;">可使用窗口的底部位置</view>
					</view>
					<view class="c-list-cell-db">
						<input class="c-input" type="text" :disabled="true" placeholder="未获取" :value="systemInfo.windowBottom"></input>
					</view>
				</view>
				<view class="c-list-cell">
					<view class="c-pd">
						<view class="c-label" style="width:180px;">状态栏的高度</view>
					</view>
					<view class="c-list-cell-db">
						<input class="c-input" type="text" :disabled="true" placeholder="未获取" :value="systemInfo.statusBarHeight"></input>
					</view>
				</view>
				<view class="c-list-cell">
					<view class="c-pd">
						<view class="c-label" style="width:180px;">DPI</view>
					</view>
					<view class="c-list-cell-db">
						<input class="c-input" type="text" :disabled="true" placeholder="未获取" :value="systemInfo.pixelRatio"></input>
					</view>
				</view>
			</view>
			<view class="c-padding-wrap">
				<view class="c-btn-v">
					<button type="primary" @tap="getSystemInfo">获取手机系统信息</button>
				</view>
			</view>
		</view>
	</view>
</template>
<script>
	export default {
		data() {
			return {
				title: 'getSystemInfo',
				systemInfo: {}
			}
		},
		onUnload:function(){
			this.systemInfo = {};
		},
		methods: {
			getSystemInfo: function () {
				c.getSystemInfo({
					success: (res) => {
						this.systemInfo = res
					}
				})
			}
		}
	}
</script>

<style>
	.c-pd {
		padding-left: 30upx;
	}
</style>
