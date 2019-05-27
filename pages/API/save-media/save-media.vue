<template>
	<view>
		<page-head :title="title"></page-head>
		<view class="c-padding-wrap">
			<view v-if="imagePath !== ''" class="media-box image">
				<image class="image" mode="widthFix" :src="imagePath" />
			</view>
			<button type="primary"  class="c-button" @click="saveImage">拍摄图片并保存到本地</button>
			<view v-if="videoPath !== ''" class="media-box">
				<video
					id="myVideo"
					:src="videoPath"
					@error="videoErrorCallback"
					enable-danmu
					danmu-btn
					controls
				></video>
			</view>
			<button type="primary" class="c-button" @click="saveVideo">录制视频并保存到本地</button>
		</view>
	</view>
</template>
<script>
export default {
	data() {
		return {
			title: 'saveImage/saveVideo',
			imagePath: '',
			videoPath: ''
		};
	},
	onLoad() {},
	methods: {
		videoErrorCallback: function(e) {
			c.showModal({
				content: e.target.errMsg,
				showCancel: false
			});
		},
		saveImage() {
			c.chooseImage({
				count: 1,
				sourceType: ['camera'],
				success: res => {
					this.imagePath = res.tempFilePaths[0];
					this.getTempFilePath(res.tempFilePaths[0], 'imageTempPath');
				}
			});
		},
		saveVideo() {
			let _this = this;
			c.chooseVideo({
				count: 1,
				sourceType: ['camera'],
				success: res => {
					console.log(res.tempFilePath)
					this.videoPath = res.tempFilePath;
					this.getTempFilePath(res.tempFilePath, 'videoTempPath');
				}
			});
		},

		getTempFilePath(url, types) {
			// 如果已经下载本地路径，那么直接储存
			let obj = {
				filePath: url,
				success: () => {
					console.log('save success');
					c.showModal({
						content: '保存成功',
						showCancel: false
					});
					c.hideLoading();
				},
				fail: e => {
					c.hideLoading();
					c.showModal({
						content: '保存失败',
						showCancel: false
					});
				}
			};
			c.showLoading({
				title: '保存中...'
			});
			if (types === 'videoTempPath') {
				c.saveVideoToPhotosAlbum(obj);
			} else {
				c.saveImageToPhotosAlbum(obj);
			}
		}
	}
};
</script>

<style>
.media-box {
	display: flex;
	justify-content: center;
	align-items: center;
	margin: 30upx 0;
	width: 100%;
}
.image {
	height: 400upx;
	overflow: hidden;
}
.image image {
	width: 100%;
	height: 100%;
}
video {
	width: 100%;
}
.c-button {
	margin: 30upx 0;
}
</style>
