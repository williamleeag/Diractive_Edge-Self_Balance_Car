<template>
    <view :class="utils.bem('radio', [direction]) + ' custom-class'">
        <view v-if="labelPosition === 'left'" :class="utils.bem('radio__label', [labelPosition, { disabled: disabled || parentDisabled }]) + ' label-class'" @tap="onClickLabel">
            <slot />
        </view>
        <view class="van-radio__icon-wrap" :style="'font-size: ' + utils.addUnit(iconSize)" @tap="onChange">
            <slot v-if="useIconSlot" name="icon" />
            <van-icon
                v-else
                name="success"
                :class="utils.bem('radio__icon', [shape, { disabled: disabled || parentDisabled, checked: valueClone === name }])"
                :style="computed.iconStyle({ iconSize, checkedColor, disabled, parentDisabled, valueClone, name })"
                custom-class="icon-class"
                :custom-style="computed.iconCustomStyle({ iconSize })"
            />
        </view>
        <view v-if="labelPosition === 'right'" :class="'label-class ' + utils.bem('radio__label', [labelPosition, { disabled: disabled || parentDisabled }])" @tap="onClickLabel">
            <slot />
        </view>
    </view>
</template>
<script module="utils" lang="wxs" src="@/miniprogram_npm/@vant/weapp/wxs/utils.wxs"></script>
<script module="computed" lang="wxs" src="@/miniprogram_npm/@vant/weapp/radio/index.wxs"></script>
<script>
'use strict';
Object.defineProperty(exports, '__esModule', {
    value: true
});
var version_1 = require('../common/version');
var component_1 = require('../common/component');
var relation_1 = require('../common/relation');
export default {
    data() {
        return {
            direction: '',
            parentDisabled: false,
            valueClone: ''
        };
    },
    field: true,
    relation: (0, relation_1.useParent)('radio-group', function () {
        this.updateFromParent();
    }),
    classes: ['icon-class', 'label-class'],
    props: {
        name: null,
        value: null,
        disabled: Boolean,
        useIconSlot: Boolean,
        checkedColor: String,
        labelPosition: {
            type: String,
            default: 'right'
        },
        labelDisabled: Boolean,
        shape: {
            type: String,
            default: 'round'
        },
        iconSize: {
            type: null,
            default: 20
        }
    },
    methods: {
        updateFromParent: function () {
            if (!this.parent) {
                return;
            }
            var _a = this.parent.data;
            var value = _a.value;
            var parentDisabled = _a.disabled;
            var direction = _a.direction;
            this.setData({
                valueClone: value,
                direction: direction,
                parentDisabled: parentDisabled
            });
        },
        emitChange: function (value) {
            var instance = this.parent || this;
            instance.$emit('input', value);
            instance.$emit('change', value);
            if ((0, version_1.canIUseModel)()) {
                instance.setData({
                    valueClone: value
                });
            }
        },
        onChange: function () {
            if (!this.disabled && !this.parentDisabled) {
                this.emitChange(this.name);
            }
        },
        onClickLabel: function () {
            var _a = this;
            var disabled = _a.disabled;
            var parentDisabled = _a.parentDisabled;
            var labelDisabled = _a.labelDisabled;
            var name = _a.name;
            if (!(disabled || parentDisabled) && !labelDisabled) {
                this.emitChange(name);
            }
        }
    },
    watch: {
        value: {
            handler: function (newVal, oldVal) {
                this.valueClone = newVal;
            },

            immediate: true
        }
    }
};
</script>
<style>
@import '../common/index.css';
.van-radio {
    align-items: center;
    display: flex;
    overflow: hidden;
    -webkit-user-select: none;
    user-select: none;
}
.van-radio__icon-wrap {
    flex: none;
}
.van-radio--horizontal {
    margin-right: var(--padding-sm, 12px);
}
.van-radio__icon {
    align-items: center;
    border: 1px solid var(--radio-border-color, #c8c9cc);
    box-sizing: border-box;
    color: transparent;
    display: flex;
    font-size: var(--radio-size, 20px);
    height: 1em;
    justify-content: center;
    text-align: center;
    transition-duration: var(--radio-transition-duration, 0.2s);
    transition-property: color, border-color, background-color;
    width: 1em;
}
.van-radio__icon--round {
    border-radius: 100%;
}
.van-radio__icon--checked {
    background-color: var(--radio-checked-icon-color, #1989fa);
    border-color: var(--radio-checked-icon-color, #1989fa);
    color: #fff;
}
.van-radio__icon--disabled {
    background-color: var(--radio-disabled-background-color, #ebedf0);
    border-color: var(--radio-disabled-icon-color, #c8c9cc);
}
.van-radio__icon--disabled.van-radio__icon--checked {
    color: var(--radio-disabled-icon-color, #c8c9cc);
}
.van-radio__label {
    word-wrap: break-word;
    color: var(--radio-label-color, #323233);
    line-height: var(--radio-size, 20px);
    padding-left: var(--radio-label-margin, 10px);
}
.van-radio__label--left {
    float: left;
    margin: 0 var(--radio-label-margin, 10px) 0 0;
}
.van-radio__label--disabled {
    color: var(--radio-disabled-label-color, #c8c9cc);
}
.van-radio__label:empty {
    margin: 0;
}
</style>
