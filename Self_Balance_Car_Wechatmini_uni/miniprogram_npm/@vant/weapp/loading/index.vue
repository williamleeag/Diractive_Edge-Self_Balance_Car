<template>
    <view :class="'custom-class ' + utils.bem('loading', { vertical })">
        <view :class="'van-loading__spinner van-loading__spinner--' + type" :style="computed.spinnerStyle({ color, size })">
            <view v-if="type === 'spinner'" class="van-loading__dot" v-for="(item, index) in array12" :key="index"></view>
        </view>
        <view class="van-loading__text" :style="computed.textStyle({ textSize })">
            <slot />
        </view>
    </view>
</template>
<script module="utils" lang="wxs" src="@/miniprogram_npm/@vant/weapp/wxs/utils.wxs"></script>
<script module="computed" lang="wxs" src="@/miniprogram_npm/@vant/weapp/loading/index.wxs"></script>
<script>
'use strict';
Object.defineProperty(exports, '__esModule', {
    value: true
});
var component_1 = require('../common/component');
export default {
    data() {
        return {
            array12: Array.from({
                length: 12
            })
        };
    },
    props: {
        color: String,
        vertical: Boolean,
        type: {
            type: String,
            default: 'circular'
        },
        size: String,
        textSize: String
    }
};
</script>
<style>
@import '../common/index.css';
:host {
    font-size: 0;
    line-height: 1;
}
.van-loading {
    align-items: center;
    color: var(--loading-spinner-color, #c8c9cc);
    display: inline-flex;
    justify-content: center;
}
.van-loading__spinner {
    animation: van-rotate var(--loading-spinner-animation-duration, 0.8s) linear infinite;
    box-sizing: border-box;
    height: var(--loading-spinner-size, 30px);
    max-height: 100%;
    max-width: 100%;
    position: relative;
    width: var(--loading-spinner-size, 30px);
}
.van-loading__spinner--spinner {
    animation-timing-function: steps(12);
}
.van-loading__spinner--circular {
    border: 1px solid transparent;
    border-radius: 100%;
    border-top-color: initial;
}
.van-loading__text {
    color: var(--loading-text-color, #969799);
    font-size: var(--loading-text-font-size, 14px);
    line-height: var(--loading-text-line-height, 20px);
    margin-left: var(--padding-xs, 8px);
}
.van-loading__text:empty {
    display: none;
}
.van-loading--vertical {
    flex-direction: column;
}
.van-loading--vertical .van-loading__text {
    margin: var(--padding-xs, 8px) 0 0;
}
.van-loading__dot {
    height: 100%;
    left: 0;
    position: absolute;
    top: 0;
    width: 100%;
}
.van-loading__dot:before {
    background-color: currentColor;
    border-radius: 40%;
    content: ' ';
    display: block;
    height: 25%;
    margin: 0 auto;
    width: 2px;
}
.van-loading__dot:first-of-type {
    opacity: 1;
    transform: rotate(30deg);
}
.van-loading__dot:nth-of-type(2) {
    opacity: 0.9375;
    transform: rotate(60deg);
}
.van-loading__dot:nth-of-type(3) {
    opacity: 0.875;
    transform: rotate(90deg);
}
.van-loading__dot:nth-of-type(4) {
    opacity: 0.8125;
    transform: rotate(120deg);
}
.van-loading__dot:nth-of-type(5) {
    opacity: 0.75;
    transform: rotate(150deg);
}
.van-loading__dot:nth-of-type(6) {
    opacity: 0.6875;
    transform: rotate(180deg);
}
.van-loading__dot:nth-of-type(7) {
    opacity: 0.625;
    transform: rotate(210deg);
}
.van-loading__dot:nth-of-type(8) {
    opacity: 0.5625;
    transform: rotate(240deg);
}
.van-loading__dot:nth-of-type(9) {
    opacity: 0.5;
    transform: rotate(270deg);
}
.van-loading__dot:nth-of-type(10) {
    opacity: 0.4375;
    transform: rotate(300deg);
}
.van-loading__dot:nth-of-type(11) {
    opacity: 0.375;
    transform: rotate(330deg);
}
.van-loading__dot:nth-of-type(12) {
    opacity: 0.3125;
    transform: rotate(1turn);
}
@keyframes van-rotate {
    0% {
        transform: rotate(0deg);
    }
    to {
        transform: rotate(1turn);
    }
}
</style>
