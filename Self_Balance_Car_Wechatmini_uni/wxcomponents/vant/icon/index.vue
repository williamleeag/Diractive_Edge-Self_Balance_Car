<template>
<uni-shadow-root class="vant-icon-index"><view :class="'custom-class '+(classPrefix)+' '+(isImageName ? 'van-icon--image' : classPrefix + '-' + name)" :style="(color ? 'color: ' + color + ';' : '')+(size ? 'font-size: ' + sizeWithUnit + ';' : '')+(customStyle)" @click="onClick">
  <van-info v-if="info !== null || dot" :dot="dot" :info="info" custom-class="van-icon__info"></van-info>
  <image v-if="isImageName" :src="name" mode="aspectFit" class="van-icon__image"></image>
</view></uni-shadow-root>
</template>

<script>
import VanInfo from '../info/index.vue'
global['__wxVueOptions'] = {components:{'van-info': VanInfo}}

global['__wxRoute'] = 'vant/icon/index'
import { VantComponent } from '../common/component';
import { addUnit } from '../common/utils';
VantComponent({
    props: {
        dot: Boolean,
        info: null,
        size: {
            type: null,
            observer: 'setSizeWithUnit'
        },
        color: String,
        customStyle: String,
        classPrefix: {
            type: String,
            value: 'van-icon'
        },
        name: {
            type: String,
            observer(val) {
                this.setData({
                    isImageName: val.indexOf('/') !== -1
                });
            }
        }
    },
    data: {
        sizeWithUnit: null,
    },
    methods: {
        onClick() {
            this.$emit('click');
        },
        setSizeWithUnit(size) {
            this.setData({
                sizeWithUnit: addUnit(size)
            });
        }
    }
});
export default global['__wxComponents']['vant/icon/index']
</script>
<style platform="mp-weixin">
@import '../common/index.css';

@font-face {
	font-weight: 400;
	font-family: vant-icon;
	font-style: normal;
	font-display: auto;
	src: url(https://img.yzcdn.cn/vant/vant-icon-0bc654.woff2) format("woff2"), url(https://img.yzcdn.cn/vant/vant-icon-0bc654.woff) format("woff"), url(https://img.yzcdn.cn/vant/vant-icon-0bc654.ttf) format("truetype")
}

.van-icon {
	position: relative;
	font: normal normal normal 14px/1 vant-icon;
	font-size: inherit;
	text-rendering: auto;
	-webkit-font-smoothing: antialiased
}

.van-icon,
.van-icon:before {
	display: inline-block
}

.van-icon-add-o:before {
	content: "\F000"
}

.van-icon-add-square:before {
	content: "\F001"
}

.van-icon-add:before {
	content: "\F002"
}

.van-icon-after-sale:before {
	content: "\F003"
}

.van-icon-aim:before {
	content: "\F004"
}

.van-icon-alipay:before {
	content: "\F005"
}

.van-icon-apps-o:before {
	content: "\F006"
}

.van-icon-arrow-down:before {
	content: "\F007"
}

.van-icon-arrow-left:before {
	content: "\F008"
}

.van-icon-arrow-up:before {
	content: "\F009"
}

.van-icon-arrow:before {
	content: "\F00A"
}

.van-icon-ascending:before {
	content: "\F00B"
}

.van-icon-audio:before {
	content: "\F00C"
}

.van-icon-award-o:before {
	content: "\F00D"
}

.van-icon-award:before {
	content: "\F00E"
}

.van-icon-bag-o:before {
	content: "\F00F"
}

.van-icon-bag:before {
	content: "\F010"
}

.van-icon-balance-list-o:before {
	content: "\F011"
}

.van-icon-balance-list:before {
	content: "\F012"
}

.van-icon-balance-o:before {
	content: "\F013"
}

.van-icon-balance-pay:before {
	content: "\F014"
}

.van-icon-bar-chart-o:before {
	content: "\F015"
}

.van-icon-bars:before {
	content: "\F016"
}

.van-icon-bell:before {
	content: "\F017"
}

.van-icon-bill-o:before {
	content: "\F018"
}

.van-icon-bill:before {
	content: "\F019"
}

.van-icon-birthday-cake-o:before {
	content: "\F01A"
}

.van-icon-bookmark-o:before {
	content: "\F01B"
}

.van-icon-bookmark:before {
	content: "\F01C"
}

.van-icon-browsing-history-o:before {
	content: "\F01D"
}

.van-icon-browsing-history:before {
	content: "\F01E"
}

.van-icon-brush-o:before {
	content: "\F01F"
}

.van-icon-bulb-o:before {
	content: "\F020"
}

.van-icon-bullhorn-o:before {
	content: "\F021"
}

.van-icon-calender-o:before {
	content: "\F022"
}

.van-icon-card:before {
	content: "\F023"
}

.van-icon-cart-circle-o:before {
	content: "\F024"
}

.van-icon-cart-circle:before {
	content: "\F025"
}

.van-icon-cart-o:before {
	content: "\F026"
}

.van-icon-cart:before {
	content: "\F027"
}

.van-icon-cash-back-record:before {
	content: "\F028"
}

.van-icon-cash-on-deliver:before {
	content: "\F029"
}

.van-icon-cashier-o:before {
	content: "\F02A"
}

.van-icon-certificate:before {
	content: "\F02B"
}

.van-icon-chart-trending-o:before {
	content: "\F02C"
}

.van-icon-chat-o:before {
	content: "\F02D"
}

.van-icon-chat:before {
	content: "\F02E"
}

.van-icon-checked:before {
	content: "\F02F"
}

.van-icon-circle:before {
	content: "\F030"
}

.van-icon-clear:before {
	content: "\F031"
}

.van-icon-clock-o:before {
	content: "\F032"
}

.van-icon-clock:before {
	content: "\F033"
}

.van-icon-close:before {
	content: "\F034"
}

.van-icon-closed-eye:before {
	content: "\F035"
}

.van-icon-cluster-o:before {
	content: "\F036"
}

.van-icon-cluster:before {
	content: "\F037"
}

.van-icon-column:before {
	content: "\F038"
}

.van-icon-comment-circle-o:before {
	content: "\F039"
}

.van-icon-comment-circle:before {
	content: "\F03A"
}

.van-icon-comment-o:before {
	content: "\F03B"
}

.van-icon-comment:before {
	content: "\F03C"
}

.van-icon-completed:before {
	content: "\F03D"
}

.van-icon-contact:before {
	content: "\F03E"
}

.van-icon-coupon-o:before {
	content: "\F03F"
}

.van-icon-coupon:before {
	content: "\F040"
}

.van-icon-credit-pay:before {
	content: "\F041"
}

.van-icon-cross:before {
	content: "\F042"
}

.van-icon-debit-pay:before {
	content: "\F043"
}

.van-icon-delete:before {
	content: "\F044"
}

.van-icon-descending:before {
	content: "\F045"
}

.van-icon-description:before {
	content: "\F046"
}

.van-icon-desktop-o:before {
	content: "\F047"
}

.van-icon-diamond-o:before {
	content: "\F048"
}

.van-icon-diamond:before {
	content: "\F049"
}

.van-icon-discount:before {
	content: "\F04A"
}

.van-icon-down:before {
	content: "\F04B"
}

.van-icon-ecard-pay:before {
	content: "\F04C"
}

.van-icon-edit:before {
	content: "\F04D"
}

.van-icon-ellipsis:before {
	content: "\F04E"
}

.van-icon-empty:before {
	content: "\F04F"
}

.van-icon-envelop-o:before {
	content: "\F050"
}

.van-icon-exchange:before {
	content: "\F051"
}

.van-icon-expand-o:before {
	content: "\F052"
}

.van-icon-expand:before {
	content: "\F053"
}

.van-icon-eye-o:before {
	content: "\F054"
}

.van-icon-eye:before {
	content: "\F055"
}

.van-icon-fail:before {
	content: "\F056"
}

.van-icon-failure:before {
	content: "\F057"
}

.van-icon-filter-o:before {
	content: "\F058"
}

.van-icon-fire-o:before {
	content: "\F059"
}

.van-icon-fire:before {
	content: "\F05A"
}

.van-icon-flag-o:before {
	content: "\F05B"
}

.van-icon-flower-o:before {
	content: "\F05C"
}

.van-icon-free-postage:before {
	content: "\F05D"
}

.van-icon-friends-o:before {
	content: "\F05E"
}

.van-icon-friends:before {
	content: "\F05F"
}

.van-icon-gem-o:before {
	content: "\F060"
}

.van-icon-gem:before {
	content: "\F061"
}

.van-icon-gift-card-o:before {
	content: "\F062"
}

.van-icon-gift-card:before {
	content: "\F063"
}

.van-icon-gift-o:before {
	content: "\F064"
}

.van-icon-gift:before {
	content: "\F065"
}

.van-icon-gold-coin-o:before {
	content: "\F066"
}

.van-icon-gold-coin:before {
	content: "\F067"
}

.van-icon-good-job-o:before {
	content: "\F068"
}

.van-icon-good-job:before {
	content: "\F069"
}

.van-icon-goods-collect-o:before {
	content: "\F06A"
}

.van-icon-goods-collect:before {
	content: "\F06B"
}

.van-icon-graphic:before {
	content: "\F06C"
}

.van-icon-home-o:before {
	content: "\F06D"
}

.van-icon-hot-o:before {
	content: "\F06E"
}

.van-icon-hot-sale-o:before {
	content: "\F06F"
}

.van-icon-hot-sale:before {
	content: "\F070"
}

.van-icon-hot:before {
	content: "\F071"
}

.van-icon-hotel-o:before {
	content: "\F072"
}

.van-icon-idcard:before {
	content: "\F073"
}

.van-icon-info-o:before {
	content: "\F074"
}

.van-icon-info:before {
	content: "\F075"
}

.van-icon-invition:before {
	content: "\F076"
}

.van-icon-label-o:before {
	content: "\F077"
}

.van-icon-label:before {
	content: "\F078"
}

.van-icon-like-o:before {
	content: "\F079"
}

.van-icon-like:before {
	content: "\F07A"
}

.van-icon-live:before {
	content: "\F07B"
}

.van-icon-location-o:before {
	content: "\F07C"
}

.van-icon-location:before {
	content: "\F07D"
}

.van-icon-lock:before {
	content: "\F07E"
}

.van-icon-logistics:before {
	content: "\F07F"
}

.van-icon-manager-o:before {
	content: "\F080"
}

.van-icon-manager:before {
	content: "\F081"
}

.van-icon-map-marked:before {
	content: "\F082"
}

.van-icon-medel-o:before {
	content: "\F083"
}

.van-icon-medel:before {
	content: "\F084"
}

.van-icon-more-o:before {
	content: "\F085"
}

.van-icon-more:before {
	content: "\F086"
}

.van-icon-music-o:before {
	content: "\F087"
}

.van-icon-music:before {
	content: "\F088"
}

.van-icon-new-arrival-o:before {
	content: "\F089"
}

.van-icon-new-arrival:before {
	content: "\F08A"
}

.van-icon-new-o:before {
	content: "\F08B"
}

.van-icon-new:before {
	content: "\F08C"
}

.van-icon-newspaper-o:before {
	content: "\F08D"
}

.van-icon-notes-o:before {
	content: "\F08E"
}

.van-icon-orders-o:before {
	content: "\F08F"
}

.van-icon-other-pay:before {
	content: "\F090"
}

.van-icon-paid:before {
	content: "\F091"
}

.van-icon-passed:before {
	content: "\F092"
}

.van-icon-pause-circle-o:before {
	content: "\F093"
}

.van-icon-pause-circle:before {
	content: "\F094"
}

.van-icon-pause:before {
	content: "\F095"
}

.van-icon-peer-pay:before {
	content: "\F096"
}

.van-icon-pending-payment:before {
	content: "\F097"
}

.van-icon-phone-circle-o:before {
	content: "\F098"
}

.van-icon-phone-circle:before {
	content: "\F099"
}

.van-icon-phone-o:before {
	content: "\F09A"
}

.van-icon-phone:before {
	content: "\F09B"
}

.van-icon-photo-o:before {
	content: "\F09C"
}

.van-icon-photo:before {
	content: "\F09D"
}

.van-icon-photograph:before {
	content: "\F09E"
}

.van-icon-play-circle-o:before {
	content: "\F09F"
}

.van-icon-play-circle:before {
	content: "\F0A0"
}

.van-icon-play:before {
	content: "\F0A1"
}

.van-icon-plus:before {
	content: "\F0A2"
}

.van-icon-point-gift-o:before {
	content: "\F0A3"
}

.van-icon-point-gift:before {
	content: "\F0A4"
}

.van-icon-points:before {
	content: "\F0A5"
}

.van-icon-printer:before {
	content: "\F0A6"
}

.van-icon-qr-invalid:before {
	content: "\F0A7"
}

.van-icon-qr:before {
	content: "\F0A8"
}

.van-icon-question-o:before {
	content: "\F0A9"
}

.van-icon-question:before {
	content: "\F0AA"
}

.van-icon-records:before {
	content: "\F0AB"
}

.van-icon-refund-o:before {
	content: "\F0AC"
}

.van-icon-replay:before {
	content: "\F0AD"
}

.van-icon-scan:before {
	content: "\F0AE"
}

.van-icon-search:before {
	content: "\F0AF"
}

.van-icon-send-gift-o:before {
	content: "\F0B0"
}

.van-icon-send-gift:before {
	content: "\F0B1"
}

.van-icon-service-o:before {
	content: "\F0B2"
}

.van-icon-service:before {
	content: "\F0B3"
}

.van-icon-setting-o:before {
	content: "\F0B4"
}

.van-icon-setting:before {
	content: "\F0B5"
}

.van-icon-share:before {
	content: "\F0B6"
}

.van-icon-shop-collect-o:before {
	content: "\F0B7"
}

.van-icon-shop-collect:before {
	content: "\F0B8"
}

.van-icon-shop-o:before {
	content: "\F0B9"
}

.van-icon-shop:before {
	content: "\F0BA"
}

.van-icon-shopping-cart-o:before {
	content: "\F0BB"
}

.van-icon-shopping-cart:before {
	content: "\F0BC"
}

.van-icon-shrink:before {
	content: "\F0BD"
}

.van-icon-sign:before {
	content: "\F0BE"
}

.van-icon-smile-comment-o:before {
	content: "\F0BF"
}

.van-icon-smile-comment:before {
	content: "\F0C0"
}

.van-icon-smile-o:before {
	content: "\F0C1"
}

.van-icon-smile:before {
	content: "\F0C2"
}

.van-icon-star-o:before {
	content: "\F0C3"
}

.van-icon-star:before {
	content: "\F0C4"
}

.van-icon-stop-circle-o:before {
	content: "\F0C5"
}

.van-icon-stop-circle:before {
	content: "\F0C6"
}

.van-icon-stop:before {
	content: "\F0C7"
}

.van-icon-success:before {
	content: "\F0C8"
}

.van-icon-thumb-circle-o:before {
	content: "\F0C9"
}

.van-icon-thumb-circle:before {
	content: "\F0CA"
}

.van-icon-todo-list-o:before {
	content: "\F0CB"
}

.van-icon-todo-list:before {
	content: "\F0CC"
}

.van-icon-tosend:before {
	content: "\F0CD"
}

.van-icon-tv-o:before {
	content: "\F0CE"
}

.van-icon-umbrella-circle:before {
	content: "\F0CF"
}

.van-icon-underway-o:before {
	content: "\F0D0"
}

.van-icon-underway:before {
	content: "\F0D1"
}

.van-icon-upgrade:before {
	content: "\F0D2"
}

.van-icon-user-circle-o:before {
	content: "\F0D3"
}

.van-icon-user-o:before {
	content: "\F0D4"
}

.van-icon-video-o:before {
	content: "\F0D5"
}

.van-icon-video:before {
	content: "\F0D6"
}

.van-icon-vip-card-o:before {
	content: "\F0D7"
}

.van-icon-vip-card:before {
	content: "\F0D8"
}

.van-icon-volume-o:before {
	content: "\F0D9"
}

.van-icon-volume:before {
	content: "\F0DA"
}

.van-icon-wap-home-o:before {
	content: "\F0DB"
}

.van-icon-wap-home:before {
	content: "\F0DC"
}

.van-icon-wap-nav:before {
	content: "\F0DD"
}

.van-icon-warn-o:before {
	content: "\F0DE"
}

.van-icon-warning-o:before {
	content: "\F0DF"
}

.van-icon-warning:before {
	content: "\F0E0"
}

.van-icon-weapp-nav:before {
	content: "\F0E1"
}

.van-icon-wechat:before {
	content: "\F0E2"
}

.van-icon-youzan-shield:before {
	content: "\F0E3"
}

.vant-icon-index {
	display: -webkit-inline-flex;
	display: inline-flex;
	-webkit-align-items: center;
	align-items: center;
	-webkit-justify-content: center;
	justify-content: center
}

.van-icon--image {
	width: 1em;
	height: 1em
}

.van-icon__image {
	width: 100%;
	height: 100%
}

.van-icon__info {
	z-index: 1
}
</style>