<template>
	<view>
		<view class="banner" @click="goDetail(banner)">
			<image class="banner-img" :src="banner.cover"></image>
			<view class="banner-title">{{ banner.title }}</view>
		</view>
		<view class="c-list">
			<view class="c-list-cell" hover-class="c-list-cell-hover" v-for="(value, key) in listData" :key="key" @click="goDetail(value)">
				<view class="c-media-list">
					<image class="c-media-list-logo" :src="value.cover"></image>
					<view class="c-media-list-body">
						<view class="c-media-list-text-top">{{ value.title }}</view>
						<view class="c-media-list-text-bottom">
							<text>{{ value.author_name }}</text>
							<text>{{ value.published_at }}</text>
						</view>
					</view>
				</view>
			</view>
		</view>
		<c-load-more :status="status" :content-text="contentText" />
	</view>
</template>

<script>
import uniLoadMore from '@/components/c-load-more/c-load-more.vue';
var dateUtils = require('../../../common/util.js').dateUtils;

export default {
	components: {
		uniLoadMore
	},
	data() {
		return {
			banner: {},
			listData: [],
			last_id: '',
			reload: false,
			status: 'more',
			contentText: {
				contentdown: '上拉加载更多',
				contentrefresh: '加载中',
				contentnomore: '没有更多'
			}
		};
	},
	onLoad() {
		this.getBanner();
		this.getList();
	},
	onPullDownRefresh() {
		this.reload = true;
		this.last_id = '';
		this.getBanner();
		this.getList();
	},
	onReachBottom() {
		this.status = 'more';
		this.getList();
	},
	methods: {
		getBanner() {
			let data = {
				column: 'id,post_id,title,author_name,cover,published_at' //需要的字段名
			};
			c.request({
				url: 'https://unidemo.dcloud.net.cn/api/banner/36kr',
				data: data,
				success: data => {
					c.stopPullDownRefresh();
					if (data.statusCode == 200) {
						this.banner = data.data;
					}
				},
				fail: (data, code) => {
					console.log('fail' + JSON.stringify(data));
				}
			});
		},
		getList() {
			var data = {
				column: 'id,post_id,title,author_name,cover,published_at' //需要的字段名
			};
			if (this.last_id) {
				//说明已有数据，目前处于上拉加载
				this.status = 'loading';
				data.minId = this.last_id;
				data.time = new Date().getTime() + '';
				data.pageSize = 10;
			}
			c.request({
				url: 'https://unidemo.dcloud.net.cn/api/news',
				data: data,
				success: data => {
					if (data.statusCode == 200) {
						let list = this.setTime(data.data);
						this.listData = this.reload ? list : this.listData.concat(list);
						this.last_id = list[list.length - 1].id;
						this.reload = false;
					}
				},
				fail: (data, code) => {
					console.log('fail' + JSON.stringify(data));
				}
			});
		},
		goDetail: function(e) {
			// 				if (!/前|刚刚/.test(e.published_at)) {
			// 					e.published_at = dateUtils.format(e.published_at);
			// 				}
			let detail = {
				author_name: e.author_name,
				cover: e.cover,
				id: e.id,
				post_id: e.post_id,
				published_at: e.published_at,
				title: e.title
			};
			c.navigateTo({
				url: '../list2detail-detail/list2detail-detail?detailDate=' + encodeURIComponent(JSON.stringify(detail))
			});
		},
		setTime: function(items) {
			var newItems = [];
			items.forEach(e => {
				newItems.push({
					author_name: e.author_name,
					cover: e.cover,
					id: e.id,
					post_id: e.post_id,
					published_at: dateUtils.format(e.published_at),
					title: e.title
				});
			});
			return newItems;
		}
	}
};
</script>

<style>
.banner {
	height: 360upx;
	overflow: hidden;
	position: relative;
	background-color: #ccc;
}

.banner-img {
	width: 100%;
}

.banner-title {
	max-height: 84upx;
	overflow: hidden;
	position: absolute;
	left: 30upx;
	bottom: 30upx;
	width: 90%;
	font-size: 32upx;
	font-weight: 400;
	line-height: 42upx;
	color: white;
	z-index: 11;
}

.c-media-list-logo {
	width: 180upx;
	height: 140upx;
}

.c-media-list-body {
	height: auto;
	justify-content: space-around;
}

.c-media-list-text-top {
	height: 74upx;
	font-size: 28upx;
	overflow: hidden;
}

.c-media-list-text-bottom {
	display: flex;
	flex-direction: row;
	justify-content: space-between;
}
</style>
