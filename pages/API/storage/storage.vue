<template>
	<view>
		<page-head :title="title"></page-head>
		<view class="c-common-mt">
			<view class="c-list">
				<view class="c-list-cell">
					<view class="c-list-cell-left">
						<view class="c-label">key</view>
					</view>
					<view class="c-list-cell-db">
						<input class="c-input" type="text" placeholder="请输入key" name="key" :value="key" @input="keyChange"></input>
					</view>
				</view>
				<view class="c-list-cell">
					<view class="c-list-cell-left">
						<view class="c-label">value</view>
					</view>
					<view class="c-list-cell-db">
						<input class="c-input" type="text" placeholder="请输入value" name="data" :value="data" @input="dataChange"></input>
					</view>
				</view>
			</view>
			<view class="c-padding-wrap">
				<view class="c-btn-v">
					<button type="primary" class="btn-setstorage" @tap="setStorage">存储数据</button>
					<button @tap="getStorage">读取数据</button>
					<button @tap="clearStorage">清理数据</button>
				</view>
			</view>
		</view>
	</view>
</template>
<script>
	export default {
		data() {
			return {
				title: 'get/set/clearStorage',
				key: '',
				data: ''
			}
		},
		methods: {
			keyChange: function (e) {
				this.key = e.target.value
			},
			dataChange: function (e) {
				this.data = e.target.value
			},
			getStorage: function () {
				var key = this.key,
					data = this.data;
				if (key.length === 0) {
					c.showModal({
						title: '读取数据失败',
						content: "key 不能为空",
						showCancel:false
					})
				} else {
					c.getStorage({
						key: key,
						success: (res) => {
							c.showModal({
								title: '读取数据成功',
								content: "data: '" + res.data + "'",
								showCancel:false
							})
						},
						fail: () => {
							c.showModal({
								title: '读取数据失败',
								content: "找不到 key 对应的数据",
								showCancel:false
							})
						}
					})
				}
			},
			setStorage: function () {
				var key = this.key
				var data = this.data
				if (key.length === 0) {
					c.showModal({
						title: '保存数据失败',
						content: 'key 不能为空',
						showCancel:false
					})
				} else {
					c.setStorage({
						key: key,
						data: data,
						success: (res) => {
							c.showModal({
								title: '存储数据成功',
								content: ' ',
								showCancel:false
							})
						},
						fail: () => {
							c.showModal({
								title: '储存数据失败!',
								showCancel:false
							})
						}
					})
				}
			},
			clearStorage: function () {
				c.clearStorageSync()
				this.key = '',
					this.data = ''
				c.showModal({
					title: '清除数据成功',
					content: ' ',
					showCancel:false
				})
			}
		}
	}
</script>

<style>
	.btn-setstorage {
		background-color: #007aff;
		color: #ffffff;
	}
</style>
