<template>
	<view>
		<c-nav-bar left-icon="back" left-text="返回" title="标题" @click-left="back" :statusBar="true" />
		<view class="c-common-mt">
			本导航栏为自定义组件，并非原生导航栏。除非原生导航栏无法满足需求，否则不推荐使用自定义导航栏组件。具体参考
			<u-link href="https://ask.dcloud.net.cn/article/34921" text="https://ask.dcloud.net.cn/article/34921" :inWhiteList="true"></u-link>
		</view>
		<view class="example-title">基本用法</view>
		<c-nav-bar left-icon="back" title="标题" @click-left="back" />
		<view class="example-title">左右显示文字</view>
		<c-nav-bar left-icon="back" right-text="菜单" left-text="返回" title="标题" @click-left="back" />
		<view class="example-title">插入slot</view>
		<c-nav-bar :fixed="false" color="#333333" background-color="#FFFFFF" right-icon="scan" @click-left="showCity" @click-right="scan">
			<block slot="left">
				<view class="city">
					<view>{{ city }}</view>
					<c-icon type="arrowdown" color="#333333" size="22" />
				</view>
			</block>
			<view class="input-view">
				<c-icon type="search" size="22" color="#666666" />
				<input confirm-type="search" class="input" type="text" placeholder="输入搜索关键词" @confirm="confirm" />
			</view>
		</c-nav-bar>
	</view>
</template>

<script>
	import uniNavBar from '@/components/c-nav-bar/c-nav-bar.vue'
	import uniIcon from '@/components/c-icon/c-icon.vue'

	export default {
		components: {
			uniNavBar,
			uniIcon
		},
		data() {
			return {
				city: '北京'
			};
		},
		methods: {
			back() {
				c.navigateBack({
					delta: 1
				});
			},
			showMenu() {
				c.showToast({
					title: '菜单'
				});
			},
			clickLeft() {
				c.showToast({
					title: '左侧按钮'
				});
			},
			search() {
				c.showToast({
					title: '搜索'
				});
			},
			showCity() {
				c.showToast({
					title: '选择城市'
				});
			},
			scan() {
				c.showToast({
					title: '扫码'
				});
			},
			confirm() {
				c.showToast({
					title: '搜索'
				});
			}
		},
		onPullDownRefresh() {
			console.log('onPullDownRefresh');
			setTimeout(function() {
				c.stopPullDownRefresh();
				console.log('stopPullDownRefresh');
			}, 1000);
		}
	};
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

	page {
		display: flex;
		flex-direction: column;
		box-sizing: border-box;
		background-color: #fff;
	}

	view {
		font-size: 28upx;
		line-height: inherit;
	}

	.example {
		padding: 0 30upx 30upx;
	}

	.example-title {
		font-size: 32upx;
		line-height: 32upx;
		color: #777;
		margin: 40upx 25upx;
		position: relative;
	}

	.example .example-title {
		margin: 40upx 0;
	}

	.example-body {
		padding: 0 40upx;
	}

	.c-common-mt {
		color: #7a7e83;
		font-size: 28upx;
		padding: 30upx;
	}

	.title {
		font-size: 15px;
		line-height: 20px;
		color: #333333;
		padding: 15px;
	}

	.city {
		display: flex;
		flex-direction: row;
		align-items: center;
		justify-content: center;
		width: 100%;
		margin-left: 8px;
		white-space: nowrap;
	}

	.input-view {
		width: 92%;
		display: flex;
		background-color: #e7e7e7;
		height: 30px;
		border-radius: 15px;
		padding: 0 4%;
		flex-wrap: nowrap;
		margin: 7px 0;
		line-height: 30px;
	}

	.input-view .c-icon {
		line-height: 30px !important;
	}

	.input-view .input {
		height: 30px;
		line-height: 30px;
		width: 94%;
		padding: 0 3%;
	}
</style>