<template>
    <view>
        <textarea
            :class="utils.bem('field__control', [inputAlign, type, { disabled, error }]) + ' input-class'"
            :fixed="fixed"
            :focus="focus"
            :cursor="cursor"
            :value="innerValue"
            :auto-focus="autoFocus"
            :disabled="disabled || readonly"
            :maxlength="maxlength"
            :placeholder="placeholder"
            :placeholder-style="placeholderStyle"
            :placeholder-class="utils.bem('field__placeholder', { error, disabled })"
            :auto-height="!!autosize"
            :style="computed.inputStyle(autosize)"
            :cursor-spacing="cursorSpacing"
            :adjust-position="adjustPosition"
            :show-confirm-bar="showConfirmBar"
            :hold-keyboard="holdKeyboard"
            :selection-end="selectionEnd"
            :selection-start="selectionStart"
            :disable-default-padding="disableDefaultPadding"
            @input="onInput"
            @tap="onClickInput"
            @blur="onBlur"
            @focus="onFocus"
            @confirm="onConfirm"
            @linechange="onLineChange"
            @keyboardheightchange="onKeyboardHeightChange"
        />
    </view>
</template>

<style></style>
