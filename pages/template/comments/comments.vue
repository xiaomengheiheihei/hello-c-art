<template>
	<view>
	<page-head :title="title"></page-head>
		<view class="c-padding-wrap">
			<!-- 评论区 start -->
			<view class="c-comment">
				<view class="c-comment-list">
					<view class="c-comment-face"><image src="https://img-cdn-qiniu.dcloud.net.cn/uniapp/images/uni@2x.png" mode="widthFix"></image></view>
					<view class="c-comment-body">
						<view class="c-comment-top">
							<text>网友</text>
						</view>
						<view class="c-comment-date">
							<text>08/10 08:12</text>
						</view>
						<view class="c-comment-content">很酷的HBuilderX和c-app，开发一次既能生成小程序，又能生成App</view>
					</view>
				</view>
				<view class="c-comment-list">
					<view class="c-comment-face"><image src="https://img-cdn-qiniu.dcloud.net.cn/uniapp/images/uni@2x.png" mode="widthFix"></image></view>
					<view class="c-comment-body">
						<view class="c-comment-top">
							<text>马克一天</text>
						</view>
						<view class="c-comment-content">很强大，厉害了我的c-app!</view>
					</view>
				</view>
				<view class="c-comment-list">
					<view class="c-comment-face"><image src="https://img-cdn-qiniu.dcloud.net.cn/uniapp/images/uni@2x.png" mode="widthFix"></image></view>
					<view class="c-comment-body">
						<view class="c-comment-top">
							<text>今生缘</text>
						</view>
						<view class="c-comment-content">好牛逼的感觉，是不是小程序、App、移动端都互通了？</view>
						<view class="c-comment-date">
							<text>08/10 07:55</text>
						</view>
					</view>
				</view>
				<view class="c-comment-list">
					<view class="c-comment-face"><image src="https://img-cdn-qiniu.dcloud.net.cn/uniapp/images/uni@2x.png" mode="widthFix"></image></view>
					<view class="c-comment-body">
						<view class="c-comment-top">
							<text>小猫咪</text>
						</view>
						<view class="c-comment-content">支持国产，支持DCloud!</view>
						<view class="c-comment-date">
							<view>2天前</view><view class="c-comment-replay-btn">5回复</view>
						</view>
					</view>
				</view>
			</view>
			<!-- 评论区 end -->
		</view>
	</view>
</template>

<script>
export default {
	data() {
		return {
			title:"评论界面"
		}
	}
}
</script>

<style>

</style>
