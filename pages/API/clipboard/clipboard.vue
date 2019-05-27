<template>
	<view>
		<page-head :title="title"></page-head>
		<view class="c-padding-wrap">
			<view class="c-title">请输入剪贴板内容</view>
			<view class="c-list">
				<view class="c-list-cell">
					<input class="c-input" type="text" placeholder="请输入剪贴板内容" :value="data" @input="dataChange"></input>
				</view>
			</view>
			<view class="c-btn-v">
				<button type="primary" @click="setClipboard">存储数据</button>
				<button @tap="getClipboard">读取数据</button>
			</view>
		</view>
	</view>
</template>
<script>
	export default {
		data() {
			return {
				title: 'get/setClipboardData',
				data: ''
			}
		},
		methods: {
			dataChange: function (e) {
				this.data = e.target.value
			},
			getClipboard: function () {
				c.getClipboardData({
					success: (res) => {
						console.log(res.data);
						const content = res.data ? '剪贴板内容为:' + res.data : '剪贴板暂无内容';
						c.showModal({
							content,
							title: '读取剪贴板',
							showCancel: false
						})
					},
					fail: () => {
						c.showModal({
							content: '读取剪贴板失败!',
							showCancel: false
						})
					}
				});
			},
			setClipboard: function () {
				var data = this.data;
				if (data.length === 0) {
					c.showModal({
						title: '设置剪贴板失败',
						content: '内容不能为空',
						showCancel: false
					})
				} else {
					c.setClipboardData({
						data: data,
						success: () => {
							// 成功处理
							// #ifdef MP-ALIPAY || MP-BAIDU || MP-TOUTIAO
							c.showToast({
								title: '设置剪贴板成功',
								icon: "success",
								mask: !1
							})
							// #endif
						},
						fail: () => {
							// 失败处理
							// #ifdef MP-ALIPAY || MP-BAIDU || MP-TOUTIAO
							c.showToast({
								title: '储存数据失败!',
								icon: "none",
								mask: !1
							})
							// #endif
						}
					});
				}
			}
		}
	}
</script>

<style>
	
</style>


