<template>
  <button
      class="ui-button"
      :class="[
      classes ? 'ui-button__' + classes : '',
      {
        'is-disabled': disabled,
      },
    ]"
      :disabled="disabled"
      @click="handleClick"
  >
    <slot v-if="$slots.default"><span></span></slot>
  </button>
</template>

<script>
export default {
  name: "Button",
  props: {
    disabled: Boolean,
    classes: {
      type: String,
      default: "",
    },
  },
  methods: {
    handleClick(evt) {
      this.$emit("click", evt);
    },
  },
};
</script>

<style lang="scss" scoped>
.ui-button {
  width: 100%;
  font-weight: bold;
  font-size: 16px;
  line-height: 19px;
  text-align: center;
  letter-spacing: 0.04em;
  text-transform: capitalize;
  color: #E7EB22;
  background: linear-gradient(135deg, #1C1E2B 0%, #323441 100%);
  box-shadow: 2px 2px 8px #0A0C15, -2px -2px 6px rgba(255, 255, 255, 0.27);
  border-radius: 5px;
  padding: 16px 15px;
  border: none;
  outline: none;
  box-sizing: border-box;
  cursor: pointer;
  transition: 0.5s;
  &.is-disabled {
    opacity: 0.4;
    pointer-events: none;
  }
  &:hover {}
  &:active {
  }
}
</style>
