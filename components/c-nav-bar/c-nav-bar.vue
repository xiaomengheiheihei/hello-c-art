<template>
	<view class="c-navbar">
		<view :class="{'c-navbar--fixed': fixed,'c-navbar--shadow':border,'c-navbar--border':border}" :style="{'background-color':backgroundColor}" class="c-navbar__content">
			<c-status-bar v-if="statusBar" />
			<view :style="{color:color}" class="c-navbar__header">
				<view class="c-navbar__header-btns" @tap="onClickLeft">
					<view v-if="leftIcon.length">
						<c-icon :type="leftIcon" :color="color" size="24" />
					</view>
					<view v-if="leftText.length" :class="{'c-navbar-btn-icon-left':!leftIcon.length}" class="c-navbar-btn-text">{{ leftText }}</view>
					<slot name="left" />
				</view>
				<view class="c-navbar__header-container">
					<view v-if="title.length" class="c-navbar__header-container-inner">{{ title }}</view>
					<!-- 标题插槽 -->
					<slot />
				</view>
				<view class="c-navbar__header-btns" @tap="onClickRight">
					<view v-if="rightIcon.length">
						<c-icon :type="rightIcon" :color="color" size="24" />
					</view>
					<!-- 优先显示图标 -->
					<view v-if="rightText.length&&!rightIcon.length" class="c-navbar-btn-text">{{ rightText }}</view>
					<slot name="right" />
				</view>
			</view>
		</view>
		<view v-if="fixed" class="c-navbar__placeholder">
			<c-status-bar v-if="statusBar" />
			<view class="c-navbar__placeholder-view" />
		</view>
	</view>
</template>

<script>
	import uniStatusBar from '../c-status-bar/c-status-bar.vue'
	import uniIcon from '../c-icon/c-icon.vue'

	export default {
		name: 'UniNavBar',
		components: {
			uniStatusBar,
			uniIcon
		},
		props: {
			title: {
				type: String,
				default: ''
			},
			leftText: {
				type: String,
				default: ''
			},
			rightText: {
				type: String,
				default: ''
			},
			leftIcon: {
				type: String,
				default: ''
			},
			rightIcon: {
				type: String,
				default: ''
			},
			fixed: {
				type: Boolean,
				default: false
			},
			color: {
				type: String,
				default: '#000000'
			},
			backgroundColor: {
				type: String,
				default: '#FFFFFF'
			},
			statusBar: {
				type: Boolean,
				default: false
			},
			shadow: {
				type: Boolean,
				default: true
			},
			border: {
				type: Boolean,
				default: true
			}
		},
		methods: {
			onClickLeft() {
				this.$emit('click-left')
			},
			onClickRight() {
				this.$emit('click-right')
			}
		}
	}
</script>

<style>
	@charset "UTF-8";

	.c-navbar__content {
		display: block;
		position: relative;
		width: 100%;
		background-color: #fff;
		overflow: hidden
	}

	.c-navbar__content view {
		line-height: 44px
	}

	.c-navbar__header {
		display: flex;
		flex-direction: row;
		width: 100%;
		height: 44px;
		line-height: 44px;
		font-size: 16px
	}

	.c-navbar__header-btns {
		display: inline-flex;
		flex-wrap: nowrap;
		flex-shrink: 0;
		width: 120upx;
		padding: 0 12upx
	}

	.c-navbar__header-btns:first-child {
		padding-left: 0
	}

	.c-navbar__header-btns:last-child {
		width: 60upx
	}

	.c-navbar__header-container {
		width: 100%;
		margin: 0 10upx
	}

	.c-navbar__header-container-inner {
		font-size: 30upx;
		text-align: center;
		padding-right: 60upx
	}

	.c-navbar__placeholder-view {
		height: 44px
	}

	.c-navbar--fixed {
		position: fixed;
		z-index: 998
	}

	.c-navbar--shadow {
		box-shadow: 0 1px 6px #ccc
	}

	.c-navbar--border:after {
		position: absolute;
		z-index: 3;
		bottom: 0;
		left: 0;
		right: 0;
		height: 1px;
		content: '';
		-webkit-transform: scaleY(.5);
		transform: scaleY(.5);
		background-color: #c8c7cc
	}
</style>