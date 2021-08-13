<template>
  <div class="input">
    <span v-if="label" class="input__label">{{ label }}</span>
    <input
        class="input__inner"
        type="text"
        :value="value"
        v-bind="$attrs"
        @input="handleInput"
        @change="handleChange"
        @keypress="handleKeyPress"
        :disabled="disabled"
        :class="[
        label ? 'input__inner_label' : '',
      ]"
    >
    <div class="input__status">{{ status }}</div>
  </div>

</template>

<script>
export default {
  name: "Input",
  props: {
    value: [String, Number],
    disabled: Boolean,
    label: {
      type: String,
      default: "",
    },
    status: {
      type: String,
      default: "",
    }
  },
  computed: {},
  methods: {
    handleInput(evt) {
      this.$emit('input', evt.target.value)
    },
    handleChange(evt) {
      this.$emit('change', evt.target.value);
    },
    handleKeyPress(evt) {
      this.$emit('keyPress', evt);
    }
  }
}
</script>

<style lang="scss" scoped>
.input {
  width: 100%;
  height: 100%;
  position: relative;
  &:not(:last-child) {
    margin-bottom: 29px;
  }
  &__label {
    font-weight: 600;
    font-size: 16px;
    line-height: 19px;
    color: #A4A7B4;
    margin-left: 15px;
  }
  &__inner {
    width: 100%;
    background: #292B38;
    font-size: 18px;
    font-weight: 600;
    line-height: 21px;
    color: #FFFFFF;
    box-shadow: inset 4px 4px 8px rgba(11, 11, 17, 0.91), inset -1px -1px 13px rgba(255, 255, 255, 0.34);
    border-radius: 50px;
    padding: 11px 25px;
    outline: 0;
    border: none;
    box-sizing: border-box;
    &::placeholder {
      color: #788aa4;
    }
    &_icon {
      padding-left: 56px;
    }
    &_label {
      margin-top: 8px;
    }
    &:disabled {
      background: #f6f5f5;
    }
  }
  &__status {
    position: absolute;
    bottom: 13px;
    right: 25px;
    font-weight: normal;
    font-size: 14px;
    line-height: 17px;
    color: #C2C9D4;
  }
}

</style>