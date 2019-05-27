<template>
	<view>
		<view class="example-title">基本用法</view>
		<c-list>
			<c-list-item :show-arrow="false" title="标题文字" />
			<c-list-item title="标题文字" />
			<c-list-item :show-badge="true" :badge-text="12" title="标题文字" />
			<c-list-item :disabled="true" :show-badge="true" :badge-text="12" title="禁用状态" />
		</c-list>
		<view class="example-title">包含描述信息</view>
		<c-list>
			<c-list-item :show-arrow="false" title="标题文字" note="描述信息" />
			<c-list-item title="标题文字" note="描述信息" />
			<c-list-item :show-badge="true" :badge-text="12" title="标题文字" note="描述信息" />
		</c-list>
		<view class="example-title">显示缩略图</view>
		<c-list>
			<c-list-item title="标题文字" thumb="https://img-cdn-qiniu.dcloud.net.cn/new-page/hx.png" />
			<c-list-item title="标题文字" note="描述信息" thumb="https://img-cdn-qiniu.dcloud.net.cn/new-page/c.png" />
		</c-list>
		<view class="example-title">显示扩展图标</view>
		<c-list>
			<c-list-item :show-extra-icon="true" :extra-icon="extraIcon1" title="标题文字" />
			<c-list-item :show-extra-icon="true" :extra-icon="extraIcon2" title="标题文字" note="描述信息" />
		</c-list>
		<view class="example-title">显示Switch</view>
		<c-list>
			<c-list-item :show-switch="true" :show-arrow="false" title="标题文字" @switchChange="switchChange" />
			<c-list-item :show-switch="true" :switch-checked="true" :show-arrow="false" title="标题文字" @switchChange="switchChange" />
			<c-list-item :disabled="true" :show-switch="true" :switch-checked="true" :show-arrow="false" title="禁用状态" @switchChange="switchChange" />
		</c-list>
	</view>
</template>

<script>
	import uniList from '@/components/c-list/c-list.vue'
	import uniListItem from '@/components/c-list-item/c-list-item.vue'

	export default {
		components: {
			uniList,
			uniListItem
		},
		data() {
			return {
				extraIcon1: {
					color: '#007aff',
					size: '22',
					type: 'info-filled'
				},
				extraIcon2: {
					color: '#4cd964',
					size: '22',
					type: 'spinner'
				}
			}
		},
		methods: {
			switchChange(e) {
				c.showToast({
					title: 'change:' + e.value,
					icon: 'none'
				})
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
</style>