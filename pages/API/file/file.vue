<template>
	<view>
		<page-head :title="title"></page-head>
		<view class="c-padding-wrap c-common-mt">
			<block v-if="tempFilePath">
				<image :src="tempFilePath" class="image" mode="aspectFit"></image>
			</block>
			<block v-if="!tempFilePath && savedFilePath">
				<image :src="savedFilePath" class="image" mode="aspectFit"></image>
			</block>
			<block v-if="!tempFilePath && !savedFilePath">
				<view class="c-hello-addfile" @click="chooseImage">+ 请选择文件</view>
			</block>
			<view class="c-btn-v">
				<button class="btn-savefile" @click="saveFile">保存文件</button>
				<button @click="clear">删除文件</button>
			</view>
			<!-- #ifndef MP-ALIPAY || MP-TOUTIAO -->
			<view class="btn-area">
				<button @click="openDocument">打开pdf文件</button>
			</view>
			<!-- #endif -->
		</view>
	</view>
</template>
<script>
	export default {
		data() {
			return {
				title: 'saveFile',
				tempFilePath: '',
				savedFilePath: ''
			}
		},
		onLoad() {
			this.savedFilePath = c.getStorageSync('savedFilePath');
		},
		methods: {
			chooseImage() {
				c.chooseImage({
					count: 1,
					success: (res) => {
						this.tempFilePath = res.tempFilePaths[0];
					}
				});
			},
			saveFile() {
				if (this.tempFilePath.length > 0) {
					c.saveFile({
						tempFilePath: this.tempFilePath,
						success: (res) => {
							this.savedFilePath = res.savedFilePath;
							c.setStorageSync('savedFilePath', res.savedFilePath);
							c.showModal({
								title: '保存成功',
								content: '下次进入页面时，此文件仍可用',
								showCancel: false
							});
						},
						fail: (res) => {
							c.showModal({
								title: '保存失败',
								content: '失败原因: ' + JSON.stringify(res),
								showCancel: false
							});
						}
					})
				} else {
					c.showModal({
						content: '请选择文件',
						showCancel: false
					});
				}
			},
			clear() {
				c.setStorageSync('savedFilePath', '');
				this.tempFilePath = '';
				this.savedFilePath = '';
			},
			// #ifndef MP-ALIPAY || MP-TOUTIAO
			openDocument() {
				c.downloadFile({
					url: 'https://raw.githubusercontent.com/mozilla/pdf.js/master/examples/learning/helloworld.pdf',
					success: (res) => {
						c.openDocument({
							filePath: res.tempFilePath,
							success: () => {
								console.log('打开文档成功');
							}
						});
					}
				});
			},
			// #endif
		}
	}
</script>

<style>
	.image {
		width: 100%;
		height: 360upx;
	}

	.btn-savefile {
		background-color: #007aff;
		color: #ffffff;
	}
</style>
