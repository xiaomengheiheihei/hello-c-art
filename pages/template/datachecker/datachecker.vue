<template>
	<view>
		<page-head :title="title"></page-head>
		<view class="c-padding-wrap">
			<form @submit="formSubmit" @reset="formReset">
				<view>
					<view class="c-title">姓名</view>
					<view class="c-list">
						<view class="c-list-cell">
							<input class="c-input" name="nickname" placeholder="请填写您的昵称" />
						</view>
					</view>
				</view>
				<view>
					<view class="c-title">性别</view>
					<radio-group class="c-flex" name="gender">
						<label>
							<radio value="男" />男</label>
						<label>
							<radio value="女" />女</label>
					</radio-group>
				</view>
				<view>
					<view class="c-title">爱好</view>
					<checkbox-group class="c-flex" name="loves">
						<label>
							<checkbox value="读书" />读书</label>
						<label>
							<checkbox value="写字" />写字</label>
					</checkbox-group>
				</view>
				<view class="c-btn-v c-common-mt">
					<button class="btn-submit" formType="submit" type="primary">Submit</button>
					<button type="default" formType="reset">Reset</button>
				</view>
			</form>
		</view>
	</view>
</template>
<script>
	//来自 graceUI 的表单验证， 使用说明见手册 http://grace.hcoder.net/doc/info/73-3.html
	var  graceChecker = require("../../../common/graceChecker.js");
	export default {
		data() {
			return {
				title: '表单验证',
			}
		},
		methods: {
			formSubmit: function (e) {
				//将下列代码加入到对应的检查位置
				//定义表单规则
				var rule = [
					{name:"nickname", checkType : "string", checkRule:"1,3",  errorMsg:"姓名应为1-3个字符"},
					{name:"gender", checkType : "in", checkRule:"男,女",  errorMsg:"请选择性别"},
					{name:"loves", checkType : "notnull", checkRule:"",  errorMsg:"请选择爱好"}
				];
				//进行表单检查
				var formData = e.detail.value;
				var checkRes = graceChecker.check(formData, rule);
				if(checkRes){
					c.showToast({title:"验证通过!", icon:"none"});
				}else{
					c.showToast({ title: graceChecker.error, icon: "none" });
				}
			},
			formReset: function (e) {
				console.log("清空数据")
				this.chosen = ''
			}
		}
	}
</script>

<style>
</style>
