<template>
	<view>
		<page-head :title="title"></page-head>
		<view class="c-padding-wrap c-common-mt">
			<form @submit="formSubmit" @reset="formReset">
				<view class="c-form-item c-column">
					<view class="title">switch</view>
					<view>
						<switch name="switch" />
					</view>
				</view>
				<view class="c-form-item c-column">
					<view class="title">radio</view>
					<radio-group name="radio">
						<label>
							<radio value="radio1" />选项一
						</label>
						<label>
							<radio value="radio2" />选项二
						</label>
					</radio-group>
				</view>
				<view class="c-form-item c-column">
					<view class="title">checkbox</view>
					<checkbox-group name="checkbox">
						<label>
							<checkbox value="checkbox1" />选项一
						</label>
						<label>
							<checkbox value="checkbox2" />选项二
						</label>
					</checkbox-group>
				</view>
				<view class="c-form-item c-column">
					<view class="title">slider</view>
					<slider value="50" name="slider" show-value></slider>
				</view>
				<view class="c-form-item c-column">
					<view class="title">input</view>
					<input class="c-input" name="input" placeholder="这是一个输入框" />
				</view>
				<view class="c-btn-v">
					<button formType="submit">Submit</button>
					<button type="default" formType="reset">Reset</button>
				</view>
			</form>
		</view>
	</view>
</template>
<script>
	export default {
		data() {
			return {
				title: 'form',
				pickerHidden: true,
				chosen: ''
			}
		},
		methods: {
			pickerConfirm: function(e) {
				this.pickerHidden = true
				this.chosen = e.target.value
			},
			pickerCancel: function(e) {
				this.pickerHidden = true
			},
			pickerShow: function(e) {
				this.pickerHidden = false
			},
			formSubmit: function(e) {
				console.log('form发生了submit事件，携带数据为：' + JSON.stringify(e.detail.value))
			},
			formReset: function(e) {
				console.log('清空数据')
				this.chosen = ''
			}
		}
	}
</script>

<style>
	.c-form-item .title {
		padding: 20upx 0;
	}
</style>
