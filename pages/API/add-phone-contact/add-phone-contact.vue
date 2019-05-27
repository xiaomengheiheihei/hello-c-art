<template>
    <view>
        <page-head :title="title"></page-head>
        <view class="c-common-mt">
            <view class="c-list">
                <view class="c-list-cell">
                    <view class="c-list-cell-left">
                        <view class="c-label">名称</view>
                    </view>
                    <view class="c-list-cell-db">
                        <input class="c-input" type="text" placeholder="请输入联系人名称" name="name" :value="name" @input="nameChange"></input>
                    </view>
                </view>
                <view class="c-list-cell">
                    <view class="c-list-cell-left">
                        <view class="c-label">手机号</view>
                    </view>
                    <view class="c-list-cell-db">
                        <input class="c-input" type="text" placeholder="请输入联系人手机号" name="phone" :value="phone" @input="phoneChange"></input>
                    </view>
                </view>
            </view>
            <view class="c-padding-wrap">
                <view class="c-btn-v">
                    <button type="primary" class="btn-setstorage" @tap="add">添加联系人</button>
                </view>
            </view>
        </view>
    </view>
</template>
<script>
    export default {
        data() {
            return {
                title: 'addPhoneContact',
                name: '',
                phone: ''
            }
        },
        methods: {
            nameChange: function(e) {
                this.name = e.detail.value
            },
            phoneChange: function(e) {
                this.phone = e.detail.value
            },
            add() {
                c.addPhoneContact({
                    firstName: this.name,
                    mobilePhoneNumber: this.phone,
                    success: function() {
                        c.showModal({
                        	content:'已成功添加联系人！',
                            showCancel:false
                        })
                    },
                    fail: function() {
                        c.showModal({
                        	content:'添加联系人失败！',
                            showCancel:false
                        })
                    }
                });
            }
        }
    }
</script>

<style>
</style>
