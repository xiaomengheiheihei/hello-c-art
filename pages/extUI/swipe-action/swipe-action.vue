<template>
	<view>
		<view class="example-title">基本用法</view>
		<c-swipe-action :options="options2" @click="bindClick">
			<view class="cont">SwipeAction 基础使用场景</view>
		</c-swipe-action>
		<view class="example-title">禁止滑动</view>
		<c-swipe-action :disabled="true">
			<view class="cont">SwipeAction 禁止滑动展示</view>
		</c-swipe-action>
		<view class="example-title">使用变量控制开关</view>
		<view class="button-view">
			<view class="button" @click="setOpened">当前状态：{{ isOpened ? '开' : '关' }}</view>
		</view>
		<c-swipe-action :options="options2" :is-opened="isOpened" :auto-close="true" @opened="bindOpened" @closed="bindClosed">
			<view class="cont">使用变量控制SwipeAction的开启状态</view>
		</c-swipe-action>
		<view class="example-title">与 List 组件一起使用</view>
		<!-- #ifndef MP-BAIDU || MP-ALIPAY || MP-TOUTIAO -->
		<c-list>
			<c-swipe-action :options="options1">
				<c-list-item :show-arrow="false" title="item1" />
			</c-swipe-action>
			<c-swipe-action :options="options2">
				<c-list-item :show-arrow="false" title="item2" />
			</c-swipe-action>
			<c-swipe-action :options="options3">
				<c-list-item :show-arrow="false" title="item3" />
			</c-swipe-action>
		</c-list>
		<!-- #endif -->
		<!-- #ifdef MP-BAIDU || MP-ALIPAY || MP-TOUTIAO -->
		<view class="c-list">
			<c-swipe-action :options="options1">
				<c-list-item :show-arrow="false" title="item1" />
			</c-swipe-action>
			<c-swipe-action :options="options2">
				<c-list-item :show-arrow="false" title="item2" />
			</c-swipe-action>
			<c-swipe-action :options="options3">
				<c-list-item :show-arrow="false" title="item3" />
			</c-swipe-action>
		</view>
		<!-- #endif -->
	</view>
</template>

<script>
	import uniSwipeAction from '@/components/c-swipe-action/c-swipe-action.vue'
	import uniList from '@/components/c-list/c-list.vue'
	import uniListItem from '@/components/c-list-item/c-list-item.vue'

	export default {
		components: {
			uniSwipeAction,
			uniList,
			uniListItem
		},
		data() {
			return {
				isOpened: false,
				options1: [{
					text: '取消置顶'
				}],
				options2: [{
					text: '取消',
					style: {
						backgroundColor: '#007aff'
					}
				}, {
					text: '确认',
					style: {
						backgroundColor: '#dd524d'
					}
				}],
				options3: [{
					text: '置顶'
				}, {
					text: '标记为已读',
					style: {
						backgroundColor: 'rgb(254,156,1)'
					}
				}, {
					text: '删除',
					style: {
						backgroundColor: 'rgb(255,58,49)'
					}
				}]
			}
		},
		methods: {
			bindClick(value) {
				c.showToast({
					title: `点击了${value.text}按钮`,
					icon: 'none'
				})
			},
			setOpened() {
				this.isOpened = !this.isOpened
			},
			bindOpened() {
				this.isOpened = true
			},
			bindClosed() {
				this.isOpened = false
			}
		}
	}
</script>

<style>
	page {
		display: flex;
		flex-direction: column;
		box-sizing: border-box;
		background-color: #fff
	}

	view {
		font-size: 28upx;
		line-height: inherit
	}

	.example {
		padding: 0 30upx 30upx
	}

	.example-title {
		font-size: 32upx;
		line-height: 32upx;
		color: #777;
		margin: 40upx 25upx;
		position: relative
	}

	.example .example-title {
		margin: 40upx 0
	}

	.example-body {
		padding: 0 40upx
	}

	.cont {
		height: 90upx;
		line-height: 90upx;
		padding: 0 30upx;
		position: relative;
	}

	.cont::before {
		position: absolute;
		z-index: 3;
		left: 0;
		right: 0;
		top: 0;
		height: 1px;
		content: '';
		transform: scaleY(0.5);
		background-color: #c8c7cc;
	}

	.cont::after {
		position: absolute;
		z-index: 3;
		left: 0;
		right: 0;
		bottom: 0;
		height: 1px;
		content: '';
		transform: scaleY(0.5);
		background-color: #c8c7cc;
	}

	.button-view {
		display: flex;
		flex-direction: row;
		justify-content: center;
		padding: 20upx 0;
	}

	.button {
		border: 1px solid #E7E7E7;
		padding: 8upx 16upx;
		border-radius: 8upx;
	}
</style>