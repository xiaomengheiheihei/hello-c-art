<template>
	<view v-if="show" :style="{backgroundColor:backgroundColor,color:color}" class="c-noticebar" @click="onClick">
		<view v-if="showClose" class="c-noticebar__close">
			<c-icon type="closefill" size="12" />
		</view>
		<view :class="{'c-noticebar--flex': scrollable || single || moreText}" class="c-noticebar__content">
			<view v-if="showIcon" :style="{backgroundColor:backgroundColor,color:color}" class="c-noticebar__content-icon">
				<c-icon :color="color" type="sound" size="14" />
			</view>
			<view :class="{'c-noticebar--scrollable':scrollable,'c-noticebar--single':!scrollable && (single || moreText)}" class="c-noticebar__content-text">
				<view :id="elId" :style="{'animation': animation,'-webkit-animation': animation}" class="c-noticebar__content-inner">{{ text }}</view>
			</view>
			<view v-if="showGetMore" :style="{width:moreText ? '180upx' : '20px'}" class="c-noticebar__content-more" @click="clickMore">
				<view v-if="moreText" class="c-noticebar__content-more-text">{{ moreText }}</view>
				<c-icon type="arrowright" size="14" />
			</view>
		</view>
	</view>
</template>

<script>
	import uniIcon from '../c-icon/c-icon.vue'
	export default {
		name: 'UniNoticeBar',
		components: {
			uniIcon
		},
		props: {
			text: {
				type: String,
				default: ''
			},
			moreText: {
				type: String,
				default: ''
			},
			backgroundColor: {
				type: String,
				default: '#fffbe8'
			},
			speed: { // 默认1s滚动100px
				type: [String, Number],
				default: 100
			},
			color: {
				type: String,
				default: '#de8c17'
			},
			single: { // 是否单行
				type: Boolean,
				default: false
			},
			scrollable: { // 是否滚动，添加后控制单行效果取消
				type: Boolean,
				default: false
			},
			showIcon: { // 是否显示左侧icon
				type: Boolean,
				default: false
			},
			showGetMore: { // 是否显示右侧查看更多
				type: Boolean,
				default: false
			},
			showClose: { // 是否显示左侧关闭按钮
				type: Boolean,
				default: false
			}
		},
		data() {
			/**
			 * TODO 兼容新旧编译器
			 * 新编译器（自定义组件模式）下必须使用固定数值，否则部分平台下会获取不到节点。
			 * 随机数值是在旧编译器下使用的，旧编译器模式已经不推荐使用，后续直接废掉随机数值的写法。
			 */
			const elId = this.__call_hook ? 'uni_notice_bar' : `Uni_${Math.ceil(Math.random() * 10e5).toString(36)}`
			return {
				elId: elId,
				show: true,
				animation: ''
			}
		},
		watch: {
			text(newValue, oldValue) {
				this.$nextTick(() => {
					setTimeout(this.setAnimation, 200)
				})
			}
		},
		// #ifdef H5
		mounted() {
			this.setAnimation()
		},
		// #endif
		// #ifndef H5
		onReady() {
			this.setAnimation()
		},
		// #endif
		methods: {
			clickMore() {
				this.$emit('getmore')
			},
			onClick(e) {
				let clientX = e.touches ? (e.touches[0] ? e.touches[0].clientX : e.changedTouches[0].clientX) : e.detail.clientX
				if (c.upx2px(48) + 12 > clientX && this.showClose) {
					this.show = false
					this.$emit('close')
				}
				this.$emit('click')
			},
			setAnimation() {
				if (!this.scrollable) {
					return
				}
				// #ifdef MP-TOUTIAO
				setTimeout(() => {
					c.createSelectorQuery().in(this).select(`#${this.elId}`).boundingClientRect().exec((ret) => {
						this.animation = `notice ${ret[0].width / this.speed}s linear infinite both`
					})
				}, 200)
				// #endif
				// #ifndef MP-TOUTIAO
				c.createSelectorQuery().in(this).select(`#${this.elId}`).boundingClientRect().exec((ret) => {
					this.animation = `notice ${ret[0].width / this.speed}s linear infinite both`
				})
				// #endif
			}
		}
	}
</script>

<style>
	@charset "UTF-8";

	.c-noticebar {
		padding: 12upx 24upx;
		font-size: 24upx;
		line-height: 1.5;
		margin-bottom: 20upx;
		display: flex;
		flex-direction: row;
		justify-content: center;
		align-items: center;
		justify-content: left
	}

	.c-noticebar__close {
		color: #999;
		margin-right: 24upx;
		display: flex;
		flex-direction: row;
		justify-content: center;
		align-items: center
	}

	.c-noticebar__content {
		flex: 1;
		overflow: hidden
	}

	.c-noticebar__content.c-noticebar--flex {
		flex: 1;
		display: flex;
		flex-direction: row
	}

	.c-noticebar__content-icon {
		display: inline-block;
		z-index: 1;
		padding-right: 12upx
	}

	.c-noticebar__content-more {
		width: 180upx;
		display: flex;
		flex-direction: row;
		justify-content: center;
		align-items: center;
		justify-content: flex-end;
		word-break: keep-all;
		margin-left: 10upx;
		color: #999
	}

	.c-noticebar__content-more-text {
		font-size: 24upx;
		white-space: nowrap
	}

	.c-noticebar__content-text {
		word-break: break-all;
		line-height: 1.5;
		display: inline
	}

	.c-noticebar__content-text.c-noticebar--single {
		text-overflow: ellipsis;
		white-space: nowrap;
		overflow: hidden
	}

	.c-noticebar__content-text.c-noticebar--scrollable {
		flex: 1;
		display: block;
		overflow: hidden
	}

	.c-noticebar__content-text.c-noticebar--scrollable .c-noticebar__content-inner {
		padding-left: 100%;
		white-space: nowrap;
		display: inline-block;
		transform: translateZ(0)
	}

	.c-noticebar__content-inner {
		font-size: 24upx;
		display: inline
	}

	@keyframes notice {
		100% {
			transform: translate3d(-100%, 0, 0)
		}
	}
</style>