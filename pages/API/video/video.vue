<template>
	<view>
		<page-head :title="title"></page-head>
		<view class="c-common-mt">
			<view class="c-list">
				<view class="c-list-cell">
					<view class="c-list-cell-left">
						<view class="c-label">视频来源</view>
					</view>
					<view class="c-list-cell-right">
						<picker :range="sourceType" @change="sourceTypeChange" :value="sourceTypeIndex">
							<view class="c-input">{{sourceType[sourceTypeIndex]}}</view>
						</picker>
					</view>
				</view>
			</view>
		</view>
		<template v-if="!src">
			<view class="c-hello-addfile" @tap="chooseVideo">+ 添加视频</view>
		</template>
		<template v-else>
			<video :src="src" class="video"></video>
		</template>
	</view>
</template>
<script>
	var sourceType = [
		['camera'],
		['album'],
		['camera', 'album']
	]
	export default {
		data() {
			return {
				title: 'chooseVideo',
				sourceTypeIndex: 2,
				sourceType: ['拍摄', '相册', '拍摄或相册'],
				src: ''
			}
		},
		onUnload(){
			this.src = '',
			this.sourceTypeIndex = 2,
			this.sourceType=['拍摄', '相册', '拍摄或相册'];
		},
		methods: {
			sourceTypeChange: function (e) {
				this.sourceTypeIndex = e.target.value
			},
			chooseVideo: function () {
				c.chooseVideo({
					sourceType: sourceType[this.sourceTypeIndex],
					success: (res) => {
						this.src = res.tempFilePath
					}
				})
			}
		}
	}
</script>

<style>
	.video{width:100%;}
</style>