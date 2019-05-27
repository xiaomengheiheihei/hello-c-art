<template>
	<view class="page">
		<page-head :title="title"></page-head>
		<view class="c-card">
			<view class="c-list">
				<view class="c-list-cell-divider">
					右侧带箭头
				</view>
				<view class="c-list-cell" hover-class="c-list-cell-hover">
					<view class="c-list-cell-navigate c-navigate-right">
						Item1
					</view>
				</view>
				<view class="c-list-cell c-list-cell-last" hover-class="c-list-cell-hover">
					<view class="c-list-cell-navigate c-navigate-right">
						Item2
					</view>
				</view>
				<view class="c-list-cell-divider">
					右侧带数字角标
				</view>
				<view class="c-list-cell" hover-class="c-list-cell-hover">
					<view class="c-list-cell-navigate">
						Item2
						<c-badge text="1" type="danger"></c-badge>
					</view>
				</view>
				<view class="c-list-cell c-list-cell-last" hover-class="c-list-cell-hover">
					<view class="c-list-cell-navigate">
						Item1
						<c-badge text="123" type="success"></c-badge>
					</view>
				</view>
				<view class="c-list-cell-divider">
					右侧带数字角标+箭头
				</view>
				<view class="c-list-cell" hover-class="c-list-cell-hover">
					<view class="c-list-cell-navigate c-navigate-right c-navigate-badge">
						Item1
						<c-badge text="123" type="success"></c-badge>
					</view>
				</view>
				<view class="c-list-cell c-list-cell-last" hover-class="c-list-cell-hover">
					<view class="c-list-cell-navigate c-navigate-right c-navigate-badge">
						Item2
						<c-badge text="12" type="primary"></c-badge>
					</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	import uniBadge from "../../../components/c-badge.vue";
	export default {
		data() {
			return {
				title: 'list-with-badges'
			}
		},
		components: {
			uniBadge
		}
	}
</script>

<style>
</style>
