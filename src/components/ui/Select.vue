<template>
  <div class="v-select">
    <div v-if="label" class="v-select__label">{{ label }}</div>
    <div class="v-select__input" :class="{'is-visible' : optionsVisible }" @click.stop="optionsVisible = !optionsVisible">
      <div :class="['v-select__inner']">
        <span> {{ _setValue }} </span>
      </div>
      <img src="../../assets/images/svg/back-icon.svg" alt="" class="v-select__icon" :class="{'rotate': optionsVisible}">
    </div>
    <div v-if="optionsVisible"
         class="v-select__options options">
      <span v-for="(option, key) in replyOptions"
            :key="key"
            class="options__item"
            :class="{'selected' : option.checked}"
            @click="selectOption(option, key)"
      >
        {{ option[labelOption] }}
      </span>
    </div>
  </div>
</template>

<script>
export default {
  name: "Select",
  props: {
    value: [String, Number, Object, Array],
    placeholder: {
      type: String,
      default: '',
    },
    options: {
      type: Array,
      default:() => []
    },
    label: {
      type: String,
      default: '',
    },
    labelOption: {
      type: String,
      default: 'name',
    },
    trackBy: {
      type: String,
      default: 'id',
    },
  },
  data() {
    return {
      optionsVisible: false,
    }
  },
  mounted() {
    document.addEventListener('click', this.hideSelect)
  },
  computed: {
    replyOptions() {
      return JSON.parse(JSON.stringify(this.options))
    },
    _setValue() {
      if(typeof this.value === 'object') {
        return this.setSelectedOption[this.labelOption]
      }else {
        return  this.placeholder
      }
    },
    setSelectedOption() {
      return this.replyOptions.filter(val => {
        val.checked = this.value[this.trackBy] === val[this.trackBy]
        if (val.checked) return val
      })[0]
    }
  },
  methods: {
    selectOption(option, key) {
      this.$emit('input', option)
      this.hideSelect()
    },
    hideSelect() {
      this.optionsVisible = false
    },
  },
  beforeDestroy() {
    document.removeEventListener('click', this.hideSelect)
  }
}
</script>

<style lang="scss" scoped>
.v-select {
  position: relative;
  width: 100%;
  margin-bottom: 29px;
  &__label {
    font-weight: 600;
    font-size: 16px;
    line-height: 19px;
    color: #A4A7B4;
    margin-left: 15px;
    margin-bottom: 8px;
  }
  &__container {
    position: relative;
  }
  &__icon {
    position: absolute;
    top: calc(50% + 13px);
    transform: translateY(-50%) rotate(-90deg);
    right: 25px;
    width: 10px;
    transition: all .3s;
    &.rotate {
      transform: translateY(-50%) rotate(90deg);
    }
  }
  &__input {
    min-height: 43px;
    display: flex;
    align-items: center;
    background: #292B38;
    font-size: 18px;
    font-weight: 600;
    line-height: 21px;
    color: #FFFFFF;
    border-radius: 50px;
    box-shadow: 4px 4px 8px rgba(11, 11, 17, 0.91), -1px -1px 13px rgba(255, 255, 255, 0.34);
    padding: 11px  25px;
    box-sizing: border-box;
    cursor: pointer;
    &.is-visible {
      border-radius: 25px 25px 0 0 ;
    }
  }
  &__options {
    background: #292B38;
    width: 100%;
    position: absolute;
    top: 100%;
    right: 0;
    box-shadow: 4px 4px 8px rgba(11, 11, 17, 0.91), -1px -1px 13px rgba(255, 255, 255, 0.34);
    border-radius: 0 0 25px 25px;
    z-index: 9999;
    overflow: hidden;
  }

}
.options {
  border-top: 1px solid #5E6477;
  &__item {
    font-weight: 600;
    font-size: 16px;
    line-height: 19px;
    color: #FFFFFF;
    display: block;
    text-align: start;
    cursor: pointer;
    padding: 13px 25px;
    &.selected {
      background: linear-gradient(180deg, #252734 1.5%, #1A1C29 99.63%);
    }
    &:hover {
      background: linear-gradient(180deg, #252734 1.5%, #1A1C29 99.63%);
    }
  }
}
</style>