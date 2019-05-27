<template>
    <view class="page">
        <page-head :title="title"></page-head>
        <view class="c-card">
            <view class="c-list">
                <view class="c-list-cell c-collapse" v-for="(list,index) in lists" :key="index" :class="index === lists.length - 1 ? 'c-list-cell-last' : ''">
                    <view class="c-list-cell-navigate c-navigate-bottom" hover-class="c-list-cell-hover" :class="list.show ? 'c-active' : ''"
                        @click="trigerCollapse(index)">
                        {{list.title}}
                    </view>
                    <view class="c-list c-collapse" :class="list.show ? 'c-active' : ''">
                        <view class="c-list-cell" hover-class="c-list-cell-hover" v-for="(item,key) in list.item" :key="key" :class="key === list.item.length - 1 ? 'c-list-cell-last' : ''">
                            <view class="c-list-cell-navigate c-navigate-right"> {{item}} </view>
                        </view>
                    </view>
                </view>
            </view>
        </view>
    </view>
</template>

<script>
    export default {
        data() {
            return {
                title: 'list-with-collapses',
                lists: [{
                        title: "产品",
                        show: false,
                        item: ["iOS", "Android", "HTML5"]
                    },
                    {
                        title: "方案",
                        show: false,
                        item: ["PC方案", "手机方案", "TV方案"]
                    },
                    {
                        title: "新闻",
                        show: false,
                        item: ["公司新闻", "行业新闻"]
                    }
                ]
            }
        },
        methods: {
            trigerCollapse(e) {
                for (let i = 0, len = this.lists.length; i < len; ++i) {
                    if (e === i) {
                        this.lists[i].show = !this.lists[i].show;
                    } else {
                        this.lists[i].show = false;
                    }
                }

            }
        }
    }
</script>

<style>

</style>
