<template>
	<view>
		<page-head :title="title"></page-head>
		<view class="c-padding-wrap">
			<view class="c-btn-v">
				<button type="default" @tap="actionSheetTap">弹出action sheet</button>
			</view>
		</view>
	</view>
</template>
<script>
	export default {
		data() {
			return {
				title: 'action-sheet'
			}
		},
		methods: {
			actionSheetTap() {
				c.showActionSheet({
					title:'标题',
					itemList: ['item1', 'item2', 'item3', 'item4'],
					success: (e) => {
						console.log(e.tapIndex);
						c.showToast({
							title:"点击了第" + e.tapIndex + "个选项",
							icon:"none"
						})
					}
				})
			}
		}
	}
</script>
