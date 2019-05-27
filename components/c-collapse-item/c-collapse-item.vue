<template>
	<view :class="['c-collapse-cell',{'c-collapse-cell--disabled':disabled,'c-collapse-cell--open':isOpen}]" :hover-class="disabled ? '' : 'c-collapse-cell--hover'">
		<view class="c-collapse-cell__title" @click="onClick">
			<view v-if="thumb" class="c-collapse-cell__title-extra">
				<image :src="thumb" class="c-collapse-cell__title-img" />
			</view>
			<view class="c-collapse-cell__title-inner">
				<view class="c-collapse-cell__title-text">{{ title }}</view>
			</view>
			<view :class="{'c-active':isOpen,'c-collapse-cell--animation':showAnimation===true}" class="c-collapse-cell__title-arrow">
				<c-icon color="#bbb" size="20" type="arrowdown" />
			</view>
		</view>
		<view :class="{'c-collapse-cell--animation':showAnimation===true}" :style="{height:isOpen ? height : '0px'}" class="c-collapse-cell__content">
			<view :id="elId">
				<slot />
			</view>
		</view>
	</view>
</template>

<script>
	import uniIcon from '../c-icon/c-icon.vue'
	export default {
		name: 'UniCollapseItem',
		components: {
			uniIcon
		},
		props: {
			title: { // 列表标题
				type: String,
				default: ''
			},
			name: { // 唯一标识符
				type: [Number, String],
				default: 0
			},
			disabled: { // 是否禁用
				type: Boolean,
				default: false
			},
			showAnimation: { // 是否显示动画
				type: Boolean,
				default: false
			},
			open: { // 是否展开
				type: Boolean,
				default: false
			},
			thumb: { // 缩略图
				type: String,
				default: ''
			}
		},
		data() {
			/**
			 * TODO 兼容新旧编译器
			 * 新编译器（自定义组件模式）下必须使用固定数值，否则部分平台下会获取不到节点。
			 * 随机数值是在旧编译器下使用的，旧编译器模式已经不推荐使用，后续直接废掉随机数值的写法。
			 */
			const elId = this.__call_hook ? 'uni_collapse_item' : `Uni_${Math.ceil(Math.random() * 10e5).toString(36)}`
			return {
				isOpen: false,
				height: 'auto',
				elId: elId
			}
		},
		watch: {
			open(val) {
				this.isOpen = val
			}
		},
		inject: ['collapse'],
		created() {
			this.isOpen = this.open
			this.nameSync = this.name ? this.name : this.collapse.childrens.length
			this.collapse.childrens.push(this)
			if (this.collapse.accordion) {
				if (this.isOpen) {
					let lastEl = this.collapse.childrens[this.collapse.childrens.length - 2]
					if (lastEl) {
						this.collapse.childrens[this.collapse.childrens.length - 2].isOpen = false
					}
				}
			}
		},
		// #ifdef H5
		mounted() {
			this.getSize()
		},
		// #endif
		// #ifndef H5
		onReady() {
			this.getSize()
		},
		// #endif
		methods: {
			getSize() {
				if (this.showAnimation) {
					c.createSelectorQuery().in(this).select(`#${this.elId}`).boundingClientRect().exec((ret) => {
						this.height = ret[0].height + 'px'
					})
				}
			},
			onClick() {
				if (this.disabled) {
					return
				}
				if (this.collapse.accordion) {
					this.collapse.childrens.forEach(vm => {
						if (vm === this) {
							return
						}
						vm.isOpen = false
					})
				}
				this.isOpen = !this.isOpen
				this.collapse.onChange && this.collapse.onChange()
			}
		}
	}
</script>

<style>
	@charset "UTF-8";

	.c-collapse-cell {
		position: relative
	}

	.c-collapse-cell--hover {
		background-color: #f1f1f1
	}

	.c-collapse-cell--open {
		background-color: #f1f1f1
	}

	.c-collapse-cell--disabled {
		opacity: .3
	}

	.c-collapse-cell--animation {
		transition: all .3s
	}

	.c-collapse-cell:after {
		position: absolute;
		z-index: 3;
		right: 0;
		bottom: 0;
		left: 0;
		height: 1px;
		content: '';
		-webkit-transform: scaleY(.5);
		transform: scaleY(.5);
		background-color: #c8c7cc
	}

	.c-collapse-cell__title {
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

	.c-collapse-cell__title-extra {
		margin-right: 18upx;
		display: flex;
		flex-direction: row;
		justify-content: center;
		align-items: center
	}

	.c-collapse-cell__title-img {
		height: 52upx;
		width: 52upx
	}

	.c-collapse-cell__title-arrow {
		width: 20px;
		height: 20px;
		transform: rotate(0);
		transform-origin: center center
	}

	.c-collapse-cell__title-arrow.c-active {
		transform: rotate(-180deg)
	}

	.c-collapse-cell__title-inner {
		flex: 1;
		overflow: hidden;
		display: flex;
		flex-direction: column
	}

	.c-collapse-cell__title-text {
		font-size: 32upx;
		text-overflow: ellipsis;
		white-space: nowrap;
		color: inherit;
		line-height: 1.5;
		overflow: hidden
	}

	.c-collapse-cell__content {
		position: relative;
		width: 100%;
		overflow: hidden;
		background: #fff
	}

	.c-collapse-cell__content view {
		font-size: 28upx
	}
</style>