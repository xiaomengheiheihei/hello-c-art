<template>
	<view v-if="text" :class="[disabled ? 'c-tag--disabled' : '',inverted ? 'c-tag--inverted' : '',circle ? 'c-tag--circle' : '', mark ? 'c-tag--mark' : '', 'c-tag--' + size, 'c-tag--' + type]" class="c-tag" @click="_onClick">{{ text }}</view>
</template>

<script>
	export default {
		name: 'UniTag',
		props: {
			type: { // 标签类型default、primary、success、warning、danger、royal
				type: String,
				default: 'default'
			},
			size: { // 标签大小 normal, small
				type: String,
				default: 'normal'
			},
			text: {
				type: String,
				default: ''
			}, // 标签内容
			disabled: { // 是否为禁用状态
				type: Boolean,
				default: false
			},
			inverted: { // 是否为空心
				type: Boolean,
				default: false
			},
			circle: { // 是否为圆角样式
				type: Boolean,
				default: false
			},
			mark: { // 是否为标记样式
				type: Boolean,
				default: false
			}
		},
		methods: {
			_onClick() {
				if (this.disabled) {
					return
				}
				this.$emit('click')
			}
		}
	}
</script>

<style>
	@charset "UTF-8";

	.c-tag {
		box-sizing: border-box;
		padding: 0 32upx;
		height: 60upx;
		line-height: calc(60upx - 2px);
		font-size: 28upx;
		display: inline-flex;
		align-items: center;
		color: #333;
		border-radius: 6upx;
		background-color: #f8f8f8;
		border: 1px solid #f8f8f8
	}

	.c-tag--circle {
		border-radius: 30upx
	}

	.c-tag--mark {
		border-radius: 0 30upx 30upx 0
	}

	.c-tag--disabled {
		opacity: .5
	}

	.c-tag--small {
		height: 40upx;
		padding: 0 16upx;
		line-height: calc(40upx - 2px);
		font-size: 24upx
	}

	.c-tag--primary {
		color: #fff;
		background-color: #007aff;
		border: 1px solid #007aff
	}

	.c-tag--primary.c-tag--inverted {
		color: #007aff;
		background-color: #fff;
		border: 1px solid #007aff
	}

	.c-tag--success {
		color: #fff;
		background-color: #4cd964;
		border: 1px solid #4cd964
	}

	.c-tag--success.c-tag--inverted {
		color: #4cd964;
		background-color: #fff;
		border: 1px solid #4cd964
	}

	.c-tag--warning {
		color: #fff;
		background-color: #f0ad4e;
		border: 1px solid #f0ad4e
	}

	.c-tag--warning.c-tag--inverted {
		color: #f0ad4e;
		background-color: #fff;
		border: 1px solid #f0ad4e
	}

	.c-tag--error {
		color: #fff;
		background-color: #dd524d;
		border: 1px solid #dd524d
	}

	.c-tag--error.c-tag--inverted {
		color: #dd524d;
		background-color: #fff;
		border: 1px solid #dd524d
	}

	.c-tag--inverted {
		color: #333;
		background-color: #fff;
		border: 1px solid #f8f8f8
	}
</style>