<template>
	<view class="page">
		<page-head :title="title"></page-head>
		<view class="">
			<view class="c-title c-center">双栏时间轴</view>
			<view class="c-timeline" style="padding: 30upx 20upx;background-color: #fff;">
				<view class="c-timeline-item c-timeline-first-item">
					<view class="c-timeline-item-keynode">2018.05</view>
					<view class="c-timeline-item-divider"></view>
					<view class="c-timeline-item-content">c-app 立项</view>
				</view>
				<view class="c-timeline-item">
					<view class="c-timeline-item-keynode">2018.07</view>
					<view class="c-timeline-item-divider"></view>
					<view class="c-timeline-item-content">c-app 正式发布，使用vue技术，开发一次，App、小程序、H5多端同时生成</view>
				</view>
				<view class="c-timeline-item c-timeline-last-item">
					<view class="c-timeline-item-keynode">2018.10</view>
					<view class="c-timeline-item-divider"></view>
					<view class="c-timeline-item-content">c-app 支持使用 npm 安装依赖，支持微信小程序自定义组件</view>
				</view>
			</view>

			<view class="c-title c-center">单栏时间轴</view>
			<view class="c-timeline" style="padding: 30upx 20upx;background-color: #fff;">
				<view class="c-timeline-item c-timeline-first-item">
					<view class="c-timeline-item-divider"></view>
					<view class="c-timeline-item-content">
						<view>
							c-app 立项
						</view>
						<view class="datetime">
							2018.05
						</view>
					</view>
				</view>
				<view class="c-timeline-item">
					<view class="c-timeline-item-divider"></view>
					<view class="c-timeline-item-content">
						<view>c-app 正式发布，使用vue技术，开发一次，App、小程序、H5多端同时生成</view>
						<view class="datetime">2018.07</view>
					</view>
				</view>
				<view class="c-timeline-item c-timeline-last-item">
					<view class="c-timeline-item-divider"></view>
					<view class="c-timeline-item-content">
						<view>c-app 支持使用 npm 安装依赖，支持微信小程序自定义组件</view>
						<view class="datetime">2018.10</view>
					</view>
				</view>
			</view>

		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: 'timeline'
			}
		}
	}
</script>

<style>
	
</style>
