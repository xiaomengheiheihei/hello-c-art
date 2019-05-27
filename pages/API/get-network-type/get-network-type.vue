<template>
	<view>
		<page-head :title="title"></page-head>
		<view class="c-padding-wrap c-common-mt">
			<view style="background:#FFFFFF; padding:40upx;">
				<view class="c-hello-text c-center">网络状态</view>
				<block v-if="hasNetworkType === false">
					<view class="c-h2 c-center c-common-mt">未获取</view>
					<view class="c-hello-text c-center c-common-mt">请点击下面按钮获取网络状态</view>
				</block>
				<block v-if="hasNetworkType === true">
					<view class="c-h2 c-center c-common-mt">{{networkType}}</view>
				</block>
			</view>
			<view class="c-btn-v c-common-mt">
				<button type="primary" @tap="getNetworkType">获取手机网络状态</button>
				<button @tap="clear">清空</button>
			</view>
		</view>
	</view>
</template>
<script>
	export default {
		data() {
			return {
				title: 'getNetworkType',
				hasNetworkType: false,
				networkType: ''
			}
		},
		onUnload:function(){
			this.networkType = '',this.hasNetworkType = false;
		},
		methods: {
			getNetworkType: function () {
				c.getNetworkType({
					success: (res) => {
						console.log(res)
						this.hasNetworkType = true, this.networkType = res.subtype || res.networkType
					},
                    fail: () => {
                        c.showModal({
                        	content:'获取失败！',
                            showCancel:false
                        })
                    }
				})
			},
			clear: function () {
				this.hasNetworkType = false,
					this.networkType = ''
			}
		}
	}
</script>

<style>

</style>
