<template>
	<view :class="{'c-grid-no-border':!showBorder,'c-grid-no-out-border':showBorder && !showOutBorder}" class="c-grid">
		<view v-for="(items,i) in gridGroup" :key="i" class="c-grid__flex">
			<view v-for="(item,index) in items" :hover-start-time="20" :hover-stay-time="70" :key="index" :class="[index == columnNum ? 'c-grid-item-last' : '','c-grid-item-' + type]" :style="{visibility:item.seize ? 'hidden' : 'inherit'}" class="c-grid-item" hover-class="c-grid-item-hover" @click="onClick(i,index)">
				<view v-if="!item.seize" class="c-grid-item__content">
					<image :src="item.image" class="c-grid-item-image" />
					<text class="c-grid-item-text">{{ item.text }}</text>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		name: 'UniGrid',
		props: {
			options: {
				type: Array,
				default () {
					return []
				}
			},
			type: { // 布局格式，长方形oblong，正方形square
				type: String,
				default: 'square'
			},
			columnNum: { // 每一行有多少个
				type: [Number, String],
				default: 3
			},
			showOutBorder: { // 显示外边框
				type: Boolean,
				default: true
			},
			showBorder: { // 是否显示border，如果为false，showOutBorder无效
				type: Boolean,
				default: true
			}
		},
		data() {
			return {}
		},
		computed: {
			gridGroup() {
				let group = []
				let groupItem = []
				this.options && this.options.forEach((item, index) => {
					groupItem.push(item)
					if (index % this.columnNum === this.columnNum - 1) {
						group.push(groupItem)
						groupItem = []
					}
				})
				if (groupItem.length > 0) {
					if (this.columnNum > groupItem.length) {
						for (let i = 0, length = groupItem.length; i < this.columnNum - length; i++) {
							groupItem.push({
								seize: true
							})
						}
					}
					group.push(groupItem)
				}
				groupItem = null
				return group
			}
		},
		created() {
			this.columnNumber = this.gridGroup[0].length
		},
		methods: {
			onClick(index, num) {
				this.$emit('click', {
					index: index * this.columnNumber + num
				})
			}
		}
	}
</script>

<style>
	@charset "UTF-8";

	.c-grid {
		position: relative;
		display: flex;
		flex-direction: column
	}

	.c-grid__flex {
		display: flex;
		flex-direction: row
	}

	.c-grid-item {
		display: flex;
		position: relative;
		flex-direction: column;
		flex: 1
	}

	.c-grid-item:before {
		display: block;
		content: " ";
		padding-bottom: 100%
	}

	.c-grid-item:after {
		content: '';
		position: absolute;
		z-index: 1;
		transform-origin: center;
		box-sizing: border-box;
		top: -50%;
		left: -50%;
		right: -50%;
		bottom: -50%;
		border-color: #c8c7cc;
		border-style: solid;
		border-width: 1px;
		-webkit-transform: scale(.5);
		transform: scale(.5);
		border-top-width: 0;
		border-left-width: 0
	}

	.c-grid-item__content {
		position: absolute;
		left: 0;
		top: 0;
		width: 100%;
		height: 100%;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center
	}

	.c-grid-item-text {
		font-size: 32upx;
		color: #333;
		margin-top: 12upx
	}

	.c-grid-item-hover {
		background-color: #f1f1f1
	}

	.c-grid-item-image {
		width: 80upx;
		height: 80upx
	}

	.c-grid .c-grid__flex:first-child .c-grid-item:after {
		border-top-width: 1px
	}

	.c-grid .c-grid__flex .c-grid-item:first-child:after {
		border-left-width: 1px
	}

	.c-grid.c-grid-no-out-border .c-grid__flex:first-child .c-grid-item:after {
		border-top-width: 0
	}

	.c-grid.c-grid-no-out-border .c-grid__flex:last-child .c-grid-item:after {
		border-bottom-width: 0
	}

	.c-grid.c-grid-no-out-border .c-grid__flex .c-grid-item:first-child:after {
		border-left-width: 0
	}

	.c-grid.c-grid-no-out-border .c-grid__flex .c-grid-item:last-child:after {
		border-right-width: 0
	}

	.c-grid.c-grid-no-border .c-grid-item:after {
		border-width: 0
	}

	.c-grid.c-grid-no-border .c-grid__flex:first-child .c-grid-item:after {
		border-top-width: 0
	}

	.c-grid.c-grid-no-border .c-grid__flex .c-grid-item:first-child:after {
		border-left-width: 0
	}

	.c-grid-item-oblong.c-grid-item:before {
		padding-bottom: 60%
	}

	.c-grid-item-oblong .c-grid-item__content {
		flex-direction: row
	}

	.c-grid-item-oblong .c-grid-item-image {
		width: 52upx;
		height: 52upx
	}

	.c-grid-item-oblong .c-grid-item-text {
		margin-top: 0;
		margin-left: 12upx
	}
</style>