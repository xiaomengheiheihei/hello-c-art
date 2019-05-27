<template>
	<view>
		<page-head :title="title"></page-head>
		<view class="c-padding-wrap c-common-mt">
			<view class="c-hello-text c-center">请在下方输入电话号码</view>
			<input class="input c-common-mt" type="number" name="input" @input="bindInput" />
			<view class="c-btn-v c-common-mt">
				<button @tap="makePhoneCall" type="primary" :disabled="disabled">拨打</button>
			</view>
		</view>
	</view>
</template>
<script>
	export default {
		data() {
			return {
				title: 'makePhoneCall',
				disabled: true
			}
		},
		methods: {
			bindInput: function (e) {
				this.inputValue = e.target.value
				if (this.inputValue.length > 0) {
					this.disabled = false
				} else {
					this.disabled = true
				}
			},
			makePhoneCall: function () {
				c.makePhoneCall({
					phoneNumber: this.inputValue,
					success: () => {
						console.log("成功拨打电话")
					}
				})
			}
		}
	}
</script>

<style>
	.input {
		height: 119upx;
		line-height: 119upx;
		font-size: 78upx;
		border-bottom: 1upx solid #E2E2E2;
		text-align:center;
	}
</style>
