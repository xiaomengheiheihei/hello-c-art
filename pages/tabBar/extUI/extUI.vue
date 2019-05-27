<template>
	<view class="c-padding-wrap c-common-pb">
		<view class="c-header-logo">
			<image src="/static/extuiIndex.png"></image>
		</view>
		<view class="c-card" v-for="(list,index) in lists" :key="index">
			<view class="c-list">
				<view class="c-list-cell c-collapse">
					<view class="c-list-cell-navigate c-navigate-right" hover-class="c-list-cell-hover" @click="goDetailPage(list.url)">
						{{list.name}}
					</view>
				</view>
			</view>
		</view>
	</view>
</template>
<script>
	import uLink from "@/components/uLink.vue"
	export default {
		components: {
			uLink
		},
		data() {
			return {
				lists: [{
						name: "Badge 数字角标",
						url: "badge"
					},
					{
						name: "Calendar 日历",
						url: "calendar"
					},
					{
						name: "Card 卡片",
						url: "card"
					},
					// #ifdef H5 || APP-PLUS || MP-WEIXIN 
					{
						name: "Collapse 折叠面板",
						url: "collapse"
					},
					// #endif 
					{
						name: "CountDown 倒计时",
						url: "count-down"
					},
					{
						name: "Drawer 抽屉",
						url: "drawer"
					},
					{
						name: "Fab 悬浮按钮",
						url: "fab"
					},
					{
						name: "Grid 宫格",
						url: "grid"
					},
					{
						name: "Icon 图标",
						url: "icon"
					},
					// #ifndef MP-BAIDU 
					{
						name: "IndexedList 索引列表",
						url: "indexed-list"
					},
					// #endif 
					{
						name: "List 列表",
						url: "list"
					},
					{
						name: "LoadMore 加载更多",
						url: "load-more"
					},
					{
						name: "NavBar 自定义导航栏",
						url: "nav-bar"
					},
					{
						name: "NoticeBar 通告栏",
						url: "notice-bar"
					},
					{
						name: "NumberBox 数字输入框",
						url: "number-box"
					},
					{
						name: "Pagination 分页器",
						url: "pagination"
					},
					{
						name: "PopUp 弹出层",
						url: "popup"
					},
					{
						name: "Rate 评分",
						url: "rate"
					},
					{
						name: "SegmentedControl 分段器",
						url: "segmented-control"
					},
					{
						name: "Steps 步骤条",
						url: "steps"
					},
					{
						name: "SwipeAction 滑动操作",
						url: "swipe-action"
					},
					{
						name: "SwiperDot 轮播图指示点",
						url: "swiper-dot"
					},
					{
						name: "Tag 标签",
						url: "tag"
					},
				]
			};
		},
		onLoad() {
			// #ifdef APP-PLUS
			plus.nativeUI.showWaiting('加载中……');
			// #endif
		},
		onReady() {
			// #ifdef APP-PLUS
			plus.nativeUI.closeWaiting();
			// #endif
		},
		onShareAppMessage() {
			return {
				title: '欢迎体验c-app',
				path: '/pages/tabBar/extUI/extUI'
			}
		},
		onNavigationBarButtonTap(e) {
			c.navigateTo({
				url: '/pages/about/about'
			});
		},
		methods: {
			goDetailPage(path) {
				c.navigateTo({
					url: '/pages/extUI/' + path + '/' + path
				});
			}
		}
	}
</script>

<style>
	page {
		height: auto;
		min-height: 100%;
	}

	.c-card {
		box-shadow: none;
	}

	.c-list:after {
		height: 0;
	}

	.c-list:before {
		height: 0;
	}

	.c-hello-text {
		word-break: break-all;
	}
</style>