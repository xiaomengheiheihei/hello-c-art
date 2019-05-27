<template>
	<view>
		<page-head :title="title"></page-head>
		<view class="c-padding-wrap c-common-mt">
			<view class="c-btn-v">
				<button type="primary" :disabled="isOpen" @click="openBluetoothAdapter">打开蓝牙模块</button>
				<button type="primary" :disabled="!isOpen" @click="closeBluetoothAdapter">关闭蓝牙模块</button>
				<button type="primary" :disabled="!isOpen || isStarted" :loading="isStarted" @click="startBeaconDiscovery">开始搜索附近的iBeacon设备</button>
				<button type="primary" :disabled="!isStarted" @click="stopBeaconDiscovery">停止搜索附近的iBeacon设备</button>
			</view>
		</view>
		<scroll-view class="c-scroll_box" scroll-y @touchmove.stop.prevent="moveHandle" @click.stop="moveHandle">
			<view class="c-title" v-if="isStarted || deviceList.length > 0">已经发现 {{ deviceList.length }} 台设备:</view>
			<view class="c-list-box" v-for="(item, index) in deviceList" :key="item.uuid">
				<view>
					<view class="c-list_name">UUID: {{ item.uuid }}</view>
					<view class="c-list_item">major: {{ item.major }}</view>
					<view class="c-list_item">minor: {{ item.minor }}</view>
					<view class="c-list_item">rssi: {{ item.rssi }} dBm</view>
					<view class="c-list_item">accuracy: {{ item.accuracy }}</view>
					<view class="c-list_item">heading: {{ item.heading }}</view>
				</view>
			</view>
		</scroll-view>
	</view>
</template>
<script>
	// 必须符合 UUID 格式
	const DEVICE_UUID = 'A1B85ED2-D76F-4AE4-8F5D-6CCF53E4E228';
	export default {
		data() {
			return {
				title: 'iBeacon',
				isOpen: false,
				isStarted: false,
				deviceList: [],
				isPageOpened: false
			};
		},
		onLoad() {
			this.onBeaconUpdate();
		},
		onShow() {
			this.isPageOpened = true;
		},
		methods: {
			maskclose() {
				this.maskShow = false;
			},
			openBluetoothAdapter() {
				c.openBluetoothAdapter({
					success: (res) => {
						console.log('初始化蓝牙成功:' + res.errMsg);
						console.log(res);
						this.isOpen = true;
						this.deviceList = [];
					},
					fail: (err) => {
						console.log('初始化蓝牙失败，错误码：' + (err.errCode || err.errMsg));
						if (err.errCode !== 0) {
							initTypes(err.errCode, err.errMsg);
						}
					}
				});
			},
			closeBluetoothAdapter(OBJECT) {
				this.stopBeaconDiscovery();
				c.closeBluetoothAdapter({
					success: (res) => {
						this.isOpen = false;
						console.log('断开蓝牙模块成功');
					}
				});
			},
			onBeaconUpdate() {
				plus.ibeacon.onBeaconUpdate(res => {
					if (!this.isPageOpened || !this.isOpen || !this.isStarted) {
						return;
					}
					if (res.code !== 0) {
						console.log(res);
						return;
					}
					if (res.beacons && res.beacons.length > 0) {
						this.getBeacons();
					} else if (!res.connected) {
						this.deviceList = [];
					}
				});
			},
			startBeaconDiscovery() {
				plus.ibeacon.startBeaconDiscovery({
					uuids: [],
					success: (res) => {
						this.isStarted = true;
						console.log(res);
					},
					fail: (err) => {
						console.error(err);
					}
				});
			},
			stopBeaconDiscovery(types) {
				c.stopBeaconDiscovery({
					success: (res) => {
						this.isStarted = false;
					},
					fail: (err) => {
						console.error(err);
					}
				});
			},
			getBeacons() {
				c.getBeacons({
					success: (res) => {
						if (res.beacons && res.beacons.length > 0) {
							console.log(res.beacons);
							this.deviceList = res.beacons;
						}
					},
					fail: (err) => {
						console.log('获取设备服务失败，错误码：' + err.errCode);
						if (errCode.errCode !== 0) {
							initTypes(errCode.errCode);
						}
					}
				});
			}
		},
		onUnload() {
			this.isPageOpened = false;
		}
	};

	/**
	 * 判断初始化蓝牙状态
	 */
	function initTypes(code, errMsg) {
		switch (code) {
			case 10000:
				toast('未初始化蓝牙适配器');
				break;
			case 10001:
				toast('未检测到蓝牙，请打开蓝牙重试！');
				break;
			case 10002:
				toast('没有找到指定设备');
				break;
			case 10003:
				toast('连接失败');
				break;
			case 10004:
				toast('没有找到指定服务');
				break;
			case 10005:
				toast('没有找到指定特征值');
				break;
			case 10006:
				toast('当前连接已断开');
				break;
			case 10007:
				toast('当前特征值不支持此操作');
				break;
			case 10008:
				toast('其余所有系统上报的异常');
				break;
			case 10009:
				toast('Android 系统特有，系统版本低于 4.3 不支持 BLE');
				break;
			default:
				toast(errMsg);
		}
	}

	/**
	 * 弹出框封装
	 */
	function toast(content, showCancel = false) {
		c.showModal({
			title: '提示',
			content,
			showCancel
		});
	}
</script>

<style>
	.c-title {
		/* width: 100%; */
		/* height: 80upx; */
		text-align: center;
	}

	.c-mask {
		position: fixed;
		top: 0;
		left: 0;
		bottom: 0;
		display: flex;
		align-items: center;
		width: 100%;
		background: rgba(0, 0, 0, 0.6);
		padding: 0 30upx;
		box-sizing: border-box;
	}

	.c-scroll_box {
		height: 70%;
		background: #fff;
		border-radius: 20upx;
	}

	.c-list-box {
		margin: 0 20upx;
		padding: 15upx 0;
		border-bottom: 1px #f5f5f5 solid;
		box-sizing: border-box;
	}

	.c-list:last-child {
		border: none;
	}

	.c-list_name {
		font-size: 30upx;
		color: #333;
	}

	.c-list_item {
		font-size: 24upx;
		color: #555;
		line-height: 1.5;
	}

	.c-success_box {
		position: absolute;
		left: 0;
		bottom: 0;
		min-height: 100upx;
		width: 100%;
		background: #fff;
		box-sizing: border-box;
		border-top: 1px #eee solid;
	}

	.c-success_sub {
		/* width: 100%%; */
		height: 100upx;
		display: flex;
		justify-content: space-between;
		align-items: center;
		padding: 0 30upx;
	}

	.c-close_button {
		padding: 0 20upx;
		height: 60upx;
		line-height: 60upx;
		background: #ce3c39;
		color: #ffffff;
		border-radius: 10upx;
	}

	.c-success_content {
		height: 600upx;
		margin: 30upx;
		margin-top: 0;
		border: 1px #eee solid;
		padding: 30upx;
	}

	.c-content_list {
		padding-bottom: 10upx;
		border-bottom: 1px #f5f5f5 solid;
	}

	.c-tips {
		text-align: center;
		font-size: 24upx;
		color: #666;
	}
</style>
