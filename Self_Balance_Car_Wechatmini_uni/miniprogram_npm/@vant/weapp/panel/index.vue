<template>
    <view class="van-panel van-hairline--top-bottom custom-class">
        <van-cell v-if="title || desc || status" :title="title" :label="desc" :value="status" custom-class="header-class" value-class="van-panel__header-value" />
        <slot v-else name="header" />

        <view class="van-panel__content">
            <slot />
        </view>

        <view class="van-panel__footer van-hairline--top footer-class">
            <slot name="footer" />
        </view>
    </view>
</template>

<script>
'use strict';
Object.defineProperty(exports, '__esModule', {
    value: true
});
var component_1 = require('../common/component');
export default {
    data() {
        return {};
    },
    classes: ['header-class', 'footer-class'],
    props: {
        desc: String,
        title: String,
        status: String
    }
};
</script>
<style>
@import '../common/index.css';
.van-panel {
    background: var(--panel-background-color, #fff);
}
.van-panel__header-value {
    color: var(--panel-header-value-color, #ee0a24);
}
.van-panel__footer {
    padding: var(--panel-footer-padding, 8px 16px);
}
.van-panel__footer:empty {
    display: none;
}
</style>
