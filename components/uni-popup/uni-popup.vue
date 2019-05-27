<template>
	<view>
		<view v-show="show" :style="{ top: offsetTop + 'px' }" class="c-mask" @click="hide" @touchmove.stop.prevent="moveHandle" />
		<view v-show="show" :class="'c-popup-' + position + ' ' + 'c-popup-' + mode" class="c-popup">
			{{ msg }}
			<slot />
			<view v-if="position === 'middle' && mode === 'insert'" :class="{
          'c-close-bottom': buttonMode === 'bottom',
          'c-close-right': buttonMode === 'right'
        }" class=" c-icon c-icon-close" @click="closeMask" />
		</view>
	</view>
</template>

<script>
	export default {
		name: 'UniPopup',
		props: {
			/**
			 * 页面显示
			 */
			show: {
				type: Boolean,
				default: false
			},
			/**
			 * 对齐方式
			 */
			position: {
				type: String,
				// top - 顶部， middle - 居中, bottom - 底部
				default: 'middle'
			},
			/**
			 * 显示模式
			 */
			mode: {
				type: String,
				default: 'insert'
			},
			/**
			 * 额外信息
			 */
			msg: {
				type: String,
				default: ''
			},
			/**
			 * h5遮罩是否到顶
			 */
			h5Top: {
				type: Boolean,
				default: false
			},
			buttonMode: {
				type: String,
				default: 'bottom'
			}
		},
		data() {
			return {
				offsetTop: 0
			}
		},
		watch: {
			h5Top(newVal) {
				if (newVal) {
					this.offsetTop = 44
				} else {
					this.offsetTop = 0
				}
			}
		},
		created() {
			let offsetTop = 0
			// #ifdef H5
			if (!this.h5Top) {
				offsetTop = 44
			} else {
				offsetTop = 0
			}
			// #endif
			this.offsetTop = offsetTop
		},
		methods: {
			hide() {
				if (this.mode === 'insert' && this.position === 'middle') return
				this.$emit('hidePopup')
			},
			closeMask() {
				if (this.mode === 'insert') {
					this.$emit('hidePopup')
				}
			},
			moveHandle() {}
		}
	}
</script>
<style>
	.c-mask {
		position: fixed;
		z-index: 998;
		top: 0;
		right: 0;
		bottom: 0;
		left: 0;
		background-color: rgba(0, 0, 0, 0.3);
	}

	.c-popup {
		position: fixed;
		z-index: 999;
		background-color: #ffffff;
	}

	.c-popup-middle {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		top: 50%;
		left: 50%;
		transform: translate(-50%, -50%);
	}

	.c-popup-middle.c-popup-insert {
		min-width: 380upx;
		min-height: 380upx;
		max-width: 100%;
		max-height: 80%;
		transform: translate(-50%, -65%);
		background: none;
		box-shadow: none;
	}

	.c-popup-middle.c-popup-fixed {
		border-radius: 10upx;
		padding: 30upx;
	}

	.c-close-bottom,
	.c-close-right {
		position: absolute;
		bottom: -180upx;
		text-align: center;
		border-radius: 50%;
		color: #f5f5f5;
		font-size: 60upx;
		font-weight: bold;
		opacity: 0.8;
		z-index: -1;
	}

	.c-close-bottom {
		margin: auto;
		left: 0;
		right: 0;
	}

	.c-close-right {
		right: -60upx;
		top: -80upx;
	}

	.c-close-bottom:after {
		content: '';
		position: absolute;
		width: 0px;
		border: 1px #f5f5f5 solid;
		top: -200upx;
		bottom: 56upx;
		left: 50%;
		transform: translate(-50%, -0%);
		opacity: 0.8;
	}

	.c-popup-top,
	.c-popup-bottom {
		display: flex;
		align-items: center;
		justify-content: center;
	}

	.c-popup-top {
		top: 0;
		left: 0;
		width: 100%;
		height: 100upx;
		line-height: 100upx;
		text-align: center;
	}

	.c-popup-bottom {
		left: 0;
		bottom: 0;
		width: 100%;
		min-height: 100upx;
		line-height: 100upx;
		text-align: center;
	}
</style>