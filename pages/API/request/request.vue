<template>
	<view>
		<page-head :title="title"></page-head>
		<view class="c-padding-wrap c-common-mt">
			<view class="c-hello-text">
				请点击按钮向服务器发起请求
			</view>
			<view class="c-textarea c-common-mt">
				<textarea :value="res"></textarea>
			</view>
			<view class="c-btn-v c-common-mt">
				<button type="primary" @click="sendRequest" :loading="loading">发起请求（Callback）</button>
				<button type="primary" @click="sendRequest('promise')" :loading="loading">发起请求（Promise）</button>
				<button type="primary" @click="sendRequest('await')" :loading="loading">发起请求（Async/Await）</button>
			</view>
		</view>
	</view>
</template>
<script>
	const requestUrl = 'https://unidemo.dcloud.net.cn/ajax/echo/text?name=c-app'
	const duration = 2000
	export default {
		data() {
			return {
				title: 'request',
				loading: false,
				res: ''
			}
		},
		methods: {
			sendRequest(mode) {
				this.loading = true;
				switch (mode) {
					case 'promise':
						this._requestPromise();
						break;
					case 'await':
						this._requestAwait();
						break;
					default:
						this._request();
						break;
				}
			},
			_request() {
				c.request({
					url: requestUrl,
					dataType: 'text',
					data: {
						noncestr: Date.now()
					},
					success: (res) => {
						console.log('request success', res)
						c.showToast({
							title: '请求成功',
							icon: 'success',
							mask: true,
							duration: duration
						});
						this.res = '请求结果 : ' + JSON.stringify(res);
					},
					fail: (err) => {
						console.log('request fail', err);
						c.showModal({
							content: err.errMsg,
							showCancel: false
						});
					},
					complete: () => {
						this.loading = false;
					}
				});
			},
			_requestPromise() {
				c.request({
					url: requestUrl,
					dataType: 'text',
					data: {
						noncestr: Date.now()
					}
				}).then(res => {
					console.log('request success', res[1]);
					c.showToast({
						title: '请求成功',
						icon: 'success',
						mask: true,
						duration: duration
					});
					this.res = '请求结果 : ' + JSON.stringify(res[1]);

					this.loading = false;
				}).catch(err => {
					console.log('request fail', err);
					c.showModal({
						content: err.errMsg,
						showCancel: false
					});

					this.loading = false;
				});
			},
			async _requestAwait() {
				const [err, res] = await c.request({
					url: requestUrl,
					dataType: 'text',
					data: {
						noncestr: Date.now()
					}
				});
				if (err) {
					console.log('request fail', err);
					c.showModal({
						content: err.errMsg,
						showCancel: false
					});
				} else {
					console.log('request success', res)
					c.showToast({
						title: '请求成功',
						icon: 'success',
						mask: true,
						duration: duration
					});
					this.res = '请求结果 : ' + JSON.stringify(res);
				}
				this.loading = false;
			}
		}
	}
</script>
