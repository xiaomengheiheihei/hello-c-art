<template>
    <view>
        <page-head :title="title"></page-head>
        <view class="c-padding-wrap">
            <view style="background:#FFF; padding:50upx 0;">
                <view class="c-hello-text c-center">支付金额</text></view>
                <view class="c-h1 c-center c-common-mt">
                    <text class="rmbLogo">￥</text>
                    <input class="price" type="digit" :value="price" maxlength="4" @input="priceChange" />
                </view>
            </view>
            <view class="c-btn-v c-common-mt">
                <!-- #ifdef MP-WEIXIN -->
                <button type="primary" @click="weixinPay" :loading="loading">微信支付</button>
                <!-- #endif -->
                <!-- #ifdef APP-PLUS -->
                <template v-if="providerList.length > 0">
                    <button v-for="(item,index) in providerList" :key="index" @click="requestPayment(item,index)"
                        :loading="item.loading">{{item.name}}支付</button>
                </template>
                <!-- #endif -->
            </view>
        </view>
    </view>
    </view>
</template>
<script>
    export default {
        data() {
            return {
                title: 'request-payment',
                loading: false,
                price: 1,
                providerList: []
            }
        },
        onLoad: function() {
            // #ifdef APP-PLUS
            c.getProvider({
                service: "payment",
                success: (e) => {
                    console.log("payment success:" + JSON.stringify(e));
                    let providerList = [];
                    e.provider.map((value) => {
                        switch (value) {
                            case 'alipay':
                                providerList.push({
                                    name: '支付宝',
                                    id: value,
                                    loading: false
                                });
                                break;
                            case 'wxpay':
                                providerList.push({
                                    name: '微信',
                                    id: value,
                                    loading: false
                                });
                                break;
                            default:
                                break;
                        }
                    })
                    this.providerList = providerList;
                },
                fail: (e) => {
                    console.log("获取支付通道失败：", e);
                }
            });
            // #endif
        },
        methods: {
            weixinPay() {
                console.log("发起支付");
                this.loading = true;
                c.login({
                    success: (e) => {
                        console.log("login success", e);
                        c.request({
                            url: `https://unidemo.dcloud.net.cn/payment/wx/mp?code=${e.code}&amount=${this.price}`,
                            success: (res) => {
                                console.log("pay request success", res);
                                if (res.statusCode !== 200) {
                                    c.showModal({
                                        content: "支付失败，请重试！",
                                        showCancel: false
                                    });
                                    return;
                                }
                                if (res.data.ret === 0) {
                                    console.log("得到接口prepay_id", res.data.payment);
                                    let paymentData = res.data.payment;
                                    c.requestPayment({
                                        timeStamp: paymentData.timeStamp,
                                        nonceStr: paymentData.nonceStr,
                                        package: paymentData.package,
                                        signType: 'MD5',
                                        paySign: paymentData.paySign,
                                        success: (res) => {
                                            c.showToast({
                                                title: "感谢您的赞助!"
                                            })
                                        },
                                        fail: (res) => {
                                            c.showModal({
                                                content: "支付失败,原因为: " + res
                                                    .errMsg,
                                                showCancel: false
                                            })
                                        },
                                        complete: () => {
                                            this.loading = false;
                                        }
                                    })
                                } else {
                                    c.showModal({
                                        content: res.data.desc,
                                        showCancel: false
                                    })
                                }
                            },
                            fail: (e) => {
                                console.log("fail", e);
                                this.loading = false;
                                c.showModal({
                                    content: "支付失败,原因为: " + e.errMsg,
                                    showCancel: false
                                })
                            }
                        })
                    },
                    fail: (e) => {
                        console.log("fail", e);
                        this.loading = false;
                        c.showModal({
                            content: "支付失败,原因为: " + e.errMsg,
                            showCancel: false
                        })
                    }
                })
            },
            async requestPayment(e, index) {
                this.providerList[index].loading = true;
                let orderInfo = await this.getOrderInfo(e.id);
                console.log("得到订单信息", orderInfo);
                if (orderInfo.statusCode !== 200) {
                    console.log("获得订单信息失败", orderInfo);
                    c.showModal({
                        content: "获得订单信息失败",
                        showCancel: false
                    })
                    return;
                }
                c.requestPayment({
                    provider: e.id,
                    orderInfo: orderInfo.data,
                    success: (e) => {
                        console.log("success", e);
                        c.showToast({
                            title: "感谢您的赞助!"
                        })
                    },
                    fail: (e) => {
                        console.log("fail", e);
                        c.showModal({
                            content: "支付失败,原因为: " + e.errMsg,
                            showCancel: false
                        })
                    },
                    complete: () => {
                        this.providerList[index].loading = false;
                    }
                })
            },
            getOrderInfo(e) {
                let appid = "";
                // #ifdef APP-PLUS
                appid = plus.runtime.appid;
                // #endif
                let url = 'https://demo.dcloud.net.cn/payment/?payid=' + e + '&appid=' + appid + '&total=' + this.price;
                return new Promise((res) => {
                    c.request({
                        url: url,
                        success: (result) => {
                            res(result);
                        },
                        fail: (e) => {
                            res(e);
                        }
                    })
                })
            },
            priceChange(e) {
                console.log(e.detail.value)
                this.price = e.detail.value;
            }
        }
    }
</script>

<style>
    .rmbLogo {
        font-size: 40upx;
    }

    button {
        background-color: #007aff;
        color: #ffffff;
    }

    .c-h1.c-center {
        display: flex;
        flex-direction: row;
        justify-content: center;
        align-items: flex-end;
    }

    .price {
        border-bottom: 1px solid #eee;
        width: 200upx;
        height: 80upx;
        padding-bottom: 4upx;
    }

    .ipaPayBtn {
        margin-top: 30upx;
    }
</style>
