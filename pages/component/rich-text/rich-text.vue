<template>
	<view class="content">
		<page-head :title="title"></page-head>
		<view class="c-padding-wrap">
			<view class="c-title c-common-mt">
				数组类型
				<text>\nnodes属性为Array</text>
			</view>
			<view class="c-common-mt" style="background:#FFF; padding:20upx;">
				<rich-text :nodes="nodes"></rich-text>
			</view>
			<view class="c-title c-common-mt">
				字符串类型
				<text>\nnodes属性为String</text>
			</view>
			<view class="c-common-mt" style="background:#FFF; padding:20upx;">
				<rich-text :nodes="strings"></rich-text>
			</view>
		</view>
	</view>
</template>
<script>
	export default {
		data() {
			return {
				title: 'rich-text',
				nodes: [{
					name: 'div',
					attrs: {
						class: 'div-class',
						style: 'line-height: 60px; color: red; text-align:center;'
					},
					children: [{
						type: 'text',
						text: 'Hello&nbsp;c-app!'
					}]
				}],
				strings: '<div style="text-align:center;"><img src="https://img-cdn-qiniu.dcloud.net.cn/uniapp/images/uni@2x.png"/></div>'
			}
		}
	}
</script>
