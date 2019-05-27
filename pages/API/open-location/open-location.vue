<template>
	<view>
		<page-head :title="title"></page-head>
		<view class="c-common-mt">
			<form @submit="openLocation">
				<view class="c-list">
					<view class="c-list-cell">
						<view class="c-list-cell-left">
							<view class="c-label">经度</view>
						</view>
						<view class="c-list-cell-db">
							<input class="c-input" type="text" :disabled="true" value="116.39747" name="longitude"></input>
						</view>
					</view>
					<view class="c-list-cell">
						<view class="c-list-cell-left">
							<view class="c-label">纬度</view>
						</view>
						<view class="c-list-cell-db">
							<input class="c-input" type="text" :disabled="true" value="39.9085" name="latitude"></input>
						</view>
					</view>
					<view class="c-list-cell">
						<view class="c-list-cell-left">
							<view class="c-label">位置名称</view>
						</view>
						<view class="c-list-cell-db">
							<input class="c-input" type="text" :disabled="true" value="天安门" name="name"></input>
						</view>
					</view>
					<view class="c-list-cell">
						<view class="c-list-cell-left">
							<view class="c-label">详细位置</view>
						</view>
						<view class="c-list-cell-db">
							<input class="c-input" type="text" :disabled="true" value="北京市东城区东长安街" name="address"></input>
						</view>
					</view>
				</view>
				<view class="c-padding-wrap">
					<view class="c-btn-v c-common-mt">
						<button type="primary" formType="submit">查看位置</button>
					</view>
				</view>
			</form>
		</view>
	</view>
</template>
<script>
	export default {
		data() {
			return {
				title: 'openLocation'
			}
		},
		methods: {
			openLocation: function (e) {
				console.log(e)
				var value = e.target.value
				c.openLocation({
					longitude: Number(value.longitude),
					latitude: Number(value.latitude),
					name: value.name,
					address: value.address
				})
			}
		}
	}
</script>

<style>
	.c-list-cell-left {
		padding: 0 30upx;
	}
</style>
