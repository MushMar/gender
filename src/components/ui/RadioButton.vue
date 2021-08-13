<template>
    <label :class="['radio', {'is-checked': value === label}]">
      <input type="radio"
             class="radio__input"
             :value="label"
             :name="name"
             :checked="value === label"
             @change="handleChange"
      >
      <slot><span class="radio__label"></span></slot>
    </label>
</template>

<script>
export default {
  name: "vRadioButton",
  props: {
    name:[Number, String],
    value:[Number, String],
    label: String,
  },
  data() {
    return {

    }
  },
  methods: {
    handleChange(evt) {
      this.$emit('input', evt.target.value)
    }
  }
}
</script>

<style lang="scss" scoped>
.radio {
  width: 156px;
  height: 233px;
  background: linear-gradient(180deg, #353744 0%, #191B28 100%);
  box-shadow: 4px 4px 8px rgba(11, 11, 17, 0.91), -1px -1px 13px rgba(255, 255, 255, 0.34);
  border-radius: 25px;
  box-sizing: border-box;
  transition: all .2s;
  display: inline-flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-around;
  font-weight: 600;
  font-size: 16px;
  line-height: 19px;
  color: #6D707D;
  &:hover {}
  &.is-checked {
    box-shadow: inset 4px 4px 8px rgba(11, 11, 17, 0.91), inset -1px -1px 13px rgba(255, 255, 255, 0.34);
    color: #FFFFFF;
  }
  &__input {
    display: none;
  }
  &__label {}
}
</style>