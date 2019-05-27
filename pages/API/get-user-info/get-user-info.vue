<template>
	<view>
		<page-head :title="title"></page-head>
		<view class="c-padding-wrap">
			<view style="background:#FFF; padding:40upx;">
				<block v-if="hasUserInfo === false">
					<view class="c-hello-text c-center">
						<text>请点击下方按钮获取用户头像及昵称</text>
					</view>
				</block>
				<block v-if="hasUserInfo === true">
					<view class="c-h4 c-center c-common-mt">{{userInfo.nickName}}</view>
					<view style="padding:30upx 0; text-align:center;">
						<image class="userinfo-avatar" :src="userInfo.avatarUrl"></image>
					</view>
				</block>
			</view>
			<view class="c-btn-v">
				<!-- #ifdef APP-PLUS || MP-ALIPAY || MP-TOUTIAO -->
				<button type="primary" @click="getUserInfo">获取用户信息</button>
				<!-- #endif -->
				<!-- #ifdef MP-WEIXIN || MP-BAIDU -->
				<button type="primary" open-type="getUserInfo" @getuserinfo="mpGetUserInfo">获取用户信息</button>
				<!-- #endif -->
				<button @click="clear">清空</button>
			</view>
		</view>
	</view>
</template>
<script>
	import {
		mapState,
		mapMutations
	} from 'vuex'

	export default {
		data() {
			return {
				title: 'getUserInfo',
				hasUserInfo: false,
				userInfo: {}
			}
		},
		computed: {
			...mapState({
				loginProvider: state => state.loginProvider
			})
		},
		methods: {
			// 获取用户信息 API 在小程序可直接使用，在 5+App 里面需要先登录才能调用
			getUserInfo() {
				c.getUserInfo({
					provider: this.loginProvider,
					success: (result) => {
						console.log('getUserInfo success', result);
						this.hasUserInfo = true;
						this.userInfo = result.userInfo;
					},
					fail: (error) => {
						console.log('getUserInfo fail', error);
						let content = error.errMsg;
						if (~content.indexOf('c.login')) {
							content = '请在登录页面完成登录操作';
						}
						c.showModal({
							title: '获取用户信息失败',
							content: '错误原因' + content,
							showCancel: false
						});
					}
				});
			},
			mpGetUserInfo(result) {
				console.log('mpGetUserInfo', result);
				if (result.detail.errMsg !== 'getUserInfo:ok') {
					c.showModal({
						title: '获取用户信息失败',
						content: '错误原因' + result.detail.errMsg,
						showCancel: false
					});
					return;
				}
				this.hasUserInfo = true;
				this.userInfo = result.detail.userInfo;
			},
			clear() {
				this.hasUserInfo = false;
				this.userInfo = {};
			}
		}
	}
</script>

<style>
	.userinfo-avatar {
		border-radius: 128upx;
		width: 128upx;
		height: 128upx;
	}
</style>
