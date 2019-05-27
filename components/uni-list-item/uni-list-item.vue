<template>
	<view :class="disabled ? 'c-list-item--disabled' : ''" :hover-class="disabled || showSwitch ? '' : 'c-list-item--hover'" class="c-list-item" @click="onClick">
		<view class="c-list-item__container">
			<view v-if="thumb" class="c-list-item__icon">
				<image :src="thumb" class="c-list-item__icon-img" />
			</view>
			<view v-else-if="showExtraIcon" class="c-list-item__icon">
				<c-icon :color="extraIcon.color" :size="extraIcon.size" :type="extraIcon.type" />
			</view>
			<view class="c-list-item__content">
				<view class="c-list-item__content-title">{{ title }}</view>
				<view v-if="note" class="c-list-item__content-note">{{ note }}</view>
			</view>
			<view v-if="showBadge || showArrow || showSwitch" class="c-list-item__extra">
				<c-badge v-if="showBadge" :type="badgeType" :text="badgeText" />
				<switch v-if="showSwitch" :disabled="disabled" :checked="switchChecked" @change="onSwitchChange" />
				<c-icon v-if="showArrow" :size="20" color="#bbb" type="arrowright" />
			</view>
		</view>
	</view>
</template>

<script>
	import uniIcon from '../c-icon/c-icon.vue'
	import uniBadge from '../c-badge/c-badge.vue'
	export default {
		name: 'UniListItem',
		components: {
			uniIcon,
			uniBadge
		},
		props: {
			title: {
				type: String,
				default: ''
			}, // 列表标题
			note: {
				type: String,
				default: ''
			}, // 列表描述
			disabled: { // 是否禁用
				type: Boolean,
				default: false
			},
			showArrow: { // 是否显示箭头
				type: Boolean,
				default: true
			},
			showBadge: { // 是否显示数字角标
				type: Boolean,
				default: false
			},
			showSwitch: { // 是否显示Switch
				type: Boolean,
				default: false
			},
			switchChecked: { // Switch是否被选中
				type: Boolean,
				default: false
			},
			badgeText: {
				type: [String, Number],
				default: ''
			}, // badge内容
			badgeType: { // badge类型
				type: String,
				default: 'success'
			},
			thumb: {
				type: String,
				default: ''
			}, // 缩略图
			showExtraIcon: { // 是否显示扩展图标
				type: Boolean,
				default: false
			},
			extraIcon: {
				type: Object,
				default () {
					return {
						type: 'contact',
						color: '#000000',
						size: 20
					}
				}
			}
		},
		data() {
			return {

			}
		},
		methods: {
			onClick() {
				this.$emit('click')
			},
			onSwitchChange(e) {
				this.$emit('switchChange', e.detail)
			}
		}
	}
</script>

<style>
	@charset "UTF-8";

	.c-list-item {
		font-size: 32upx;
		position: relative;
		display: flex;
		flex-direction: column;
		justify-content: space-between;
		align-items: center
	}

	.c-list-item--disabled {
		opacity: .3
	}

	.c-list-item--hover {
		background-color: #f1f1f1
	}

	.c-list-item__container {
		padding: 24upx 30upx;
		width: 100%;
		box-sizing: border-box;
		flex: 1;
		position: relative;
		display: flex;
		flex-direction: row;
		justify-content: space-between;
		align-items: center
	}

	.c-list-item__container:after {
		position: absolute;
		z-index: 3;
		right: 0;
		bottom: 0;
		left: 30upx;
		height: 1px;
		content: '';
		-webkit-transform: scaleY(.5);
		transform: scaleY(.5);
		background-color: #c8c7cc
	}

	.c-list-item__content {
		flex: 1;
		overflow: hidden;
		display: flex;
		flex-direction: column
	}

	.c-list-item__content-title {
		font-size: 32upx;
		text-overflow: ellipsis;
		white-space: nowrap;
		color: inherit;
		line-height: 1.5;
		overflow: hidden
	}

	.c-list-item__content-note {
		color: #999;
		font-size: 28upx;
		white-space: normal;
		display: -webkit-box;
		-webkit-box-orient: vertical;
		-webkit-line-clamp: 2;
		overflow: hidden
	}

	.c-list-item__extra {
		width: 25%;
		display: flex;
		flex-direction: row;
		justify-content: flex-end;
		align-items: center
	}

	.c-list-item__icon {
		margin-right: 18upx;
		display: flex;
		flex-direction: row;
		justify-content: center;
		align-items: center
	}

	.c-list-item__icon-img {
		height: 52upx;
		width: 52upx
	}

	.c-list>.c-list-item:last-child .c-list-item-container:after {
		height: 0
	}
</style>