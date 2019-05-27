<template>
    <view class="page">
        <page-head :title="title"></page-head>
        <view class="c-list">
            <block v-for="(item,index) in lists" :key="index">
                <view class="c-list-cell" hover-class="c-list-cell-hover">
                    <view class="c-triplex-row">
                        <view class="c-triplex-left">
                            <text class="c-title c-ellipsis">列表主标题</text>
                            <text class="c-text">列表副标题</text>
                            <text class="c-text-small c-ellipsis">列表内容文字,列表内容文字,列表内容文字,列表内容文字,列表内容文字,列表内容文字</text>
                        </view>
                        <view class="c-triplex-right">
                            <text class="c-h5">12:15</text>
                        </view>
                    </view>
                </view>
            </block>
        </view>
    </view>
</template>

<script>
    export default {
        data() {
            return {
                title: 'list-triplex-row',
                lists: []
            }
        },
        onLoad() {
            let list = [];
            for (let i = 0; i < 5; i++) {
                list.push(i)
            }
            this.lists = list;
        }
    }
</script>

<style>
</style>
