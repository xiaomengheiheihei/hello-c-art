<template>
	<view class="c-steps">
		<view :class="'c-steps-' + direction" class="c-steps-items">
			<view v-for="(item,index) in options" :key="index" :class="{'c-steps-process':index === active,'c-steps-finish':index < active}" class="c-steps-item">
				<view :style="{color:index === active ? activeColor : ''}" class="c-steps-item-title-container">
					<view class="c-steps-item-title">{{ item.title }}</view>
					<view v-if="item.desc" class="c-steps-item-desc">{{ item.desc }}</view>
				</view>
				<view class="c-steps-item-circle-container">
					<view v-if="index !== active" :style="{backgroundColor:index < active ? activeColor : ''}" class="c-steps-item-circle" />
					<c-icon v-else :color="activeColor" type="checkbox-filled" size="14" />
				</view>
				<view v-if="index !== options.length-1" :style="{backgroundColor:index < active ? activeColor : ''}" class="c-steps-item-line" />
			</view>
		</view>
	</view>
</template>

<script>
	import uniIcon from '../c-icon/c-icon.vue'
	export default {
		name: 'UniSteps',
		components: {
			uniIcon
		},
		props: {
			direction: { // 排列方向 row column
				type: String,
				default: 'row'
			},
			activeColor: { // 激活状态颜色
				type: String,
				default: '#1aad19'
			},
			active: { // 当前步骤
				type: Number,
				default: 0
			},
			options: {
				type: Array,
				default () {
					return []
				}
			} // 数据
		},
		data() {
			return {}
		}
	}
</script>

<style>
	@charset "UTF-8";

	.c-steps {
		width: 100%;
		box-sizing: border-box;
		display: flex;
		flex-direction: column;
		overflow: hidden;
		position: relative
	}

	.c-steps-items {
		position: relative;
		display: flex;
		flex-direction: row;
		margin: 10px;
		box-sizing: border-box;
		overflow: hidden
	}

	.c-steps-items.c-steps-column {
		margin: 10px 0;
		padding-left: 31px;
		flex-direction: column
	}

	.c-steps-items.c-steps-column .c-steps-item:after {
		content: ' ';
		position: absolute;
		height: 1px;
		width: 100%;
		bottom: 9px;
		left: 0;
		background-color: #ebedf0;
		transform: scaleY(.5)
	}

	.c-steps-items.c-steps-column .c-steps-item:last-child {
		position: relative
	}

	.c-steps-items.c-steps-column .c-steps-item:last-child:after {
		height: 0
	}

	.c-steps-items.c-steps-column .c-steps-item:last-child .c-steps-item-title-container {
		text-align: left
	}

	.c-steps-items.c-steps-column .c-steps-item:last-child .c-steps-item-circle-container {
		left: -17px;
		right: auto
	}

	.c-steps-items.c-steps-column .c-steps-item-title-container {
		transform: none;
		display: block;
		line-height: 36upx
	}

	.c-steps-items.c-steps-column .c-steps-item-title {
		text-overflow: ellipsis;
		white-space: nowrap;
		overflow: hidden
	}

	.c-steps-items.c-steps-column .c-steps-item-desc {
		white-space: normal;
		display: -webkit-box;
		-webkit-box-orient: vertical;
		-webkit-line-clamp: 2;
		overflow: hidden
	}

	.c-steps-items.c-steps-column .c-steps-item-circle-container {
		left: -17px;
		top: -1px;
		bottom: auto;
		padding: 8px 0;
		z-index: 1
	}

	.c-steps-items.c-steps-column .c-steps-item-line {
		height: 100%;
		width: 1px;
		left: -15px;
		top: -1px;
		bottom: auto
	}

	.c-steps-items.c-steps-column .c-steps-item.c-steps-process .c-steps-item-circle-container {
		bottom: auto;
		left: -21px
	}

	.c-steps-item {
		flex: 1;
		position: relative;
		padding-bottom: 18px
	}

	.c-steps-item-title-container {
		text-align: left;
		margin-left: 3px;
		display: inline-block;
		transform: translateX(-50%);
		color: #999
	}

	.c-steps-item-title {
		font-size: 28upx
	}

	.c-steps-item-desc {
		font-size: 24upx
	}

	.c-steps-item:first-child .c-steps-item-title-container {
		transform: none;
		margin-left: 0
	}

	.c-steps-item:last-child {
		position: absolute;
		right: 0
	}

	.c-steps-item:last-child .c-steps-item-title-container {
		transform: none;
		text-align: right
	}

	.c-steps-item:last-child .c-steps-item-circle-container {
		left: auto;
		right: -8px
	}

	.c-steps-item-circle-container {
		position: absolute;
		bottom: 8px;
		left: -8px;
		padding: 0 8px;
		background-color: #fff;
		z-index: 1;
		line-height: normal !important
	}

	.c-steps-item-circle {
		width: 5px;
		height: 5px;
		background-color: #999;
		border-radius: 50%
	}

	.c-steps-item-line {
		background-color: #ebedf0;
		position: absolute;
		bottom: 10px;
		left: 0;
		width: 100%;
		height: 1px
	}

	.c-steps-item.c-steps-finish .c-steps-item-title-container {
		color: #333
	}

	.c-steps-item.c-steps-process .c-steps-item-circle-container {
		bottom: 3px;
		display: flex
	}
</style>