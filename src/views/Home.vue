<template>
  <div class="home">

    <div class="home__user-block user">
      <div class="user__header header">
        <div class="header__action" :class="{'is-form': isGender}">
          <div v-if="isGender" @click="toPrevSection" class="header__icon-button">
            <svg   width="10" class="header__back-icon" :fill="'#788AA4'" >
              <use xlink:href="../assets/images/svg/sprite.svg#back"></use>
            </svg>
          </div>
          <div class="header__name"> {{ userName }} </div>
        </div>

      </div>

      <transition name="slide-fade" mode="out-in">
        <div v-if="!isGender"  key="1" class="user__admin">
          <UiRadioButton name="name"  @change="getValue"  v-model="userSelect" label="Female">
            <img src="../assets/images/user-female-image.png" alt="">
            Женский
          </UiRadioButton>
          <UiRadioButton name="name"  @change="getValue"  v-model="userSelect" label="Male">
            <img src="../assets/images/user-male-icon.png" alt="">
            Мужской
          </UiRadioButton>
        </div>
        <div v-else  key="2" class="user__form">
          <UiInput v-bind="age" label="Ваш возраст" status="год(-а)/лет"  @keyPress="isInputNumber($event, age)"></UiInput>
          <UiInput v-bind="growth" label="Рост" status="см" @keyPress="isInputNumber($event, growth)"></UiInput>
          <UiInput v-bind="currentWeight" label="Текущий вес" status="кг" @keyPress="isInputNumber($event, currentWeight)"></UiInput>
          <UiSelect  v-model="targetValue" :options="options" placeholder="Выбрать" label="Цель"></UiSelect>
          <UiInput v-bind="targetWeight" label="Целевой вес" status="кг" @keyPress="isInputNumber($event, targetWeight)"></UiInput>
        </div>
      </transition>
      <div class="user__action">
        <UiButton @click="toUserForm" :disabled="isDisabledButton">Enter</UiButton>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'Home',
  components: {},
  data() {
    return {
      age: '',
      growth: '',
      currentWeight: '',
      targetWeight: '',
      isGender: false,
      userSelect: '',

      targetValue: '',
      options: [
        {
          id: 1,
          name: 'Быстрая скорость набора',
        },
        {
          id: 2,
          name: 'Средняя скорость набора',
        },
        {
          id: 3 ,
          name: 'Поддержка',
        },
        {
          id: 4,
          name: 'Средняя скорость похудения',
        },
        {
          id: 5,
          name: 'Быстрая скорость похудения',
        }
      ],
    }
  },
  computed: {
    isDisabledButton() {
      return this.userSelect === '';
    },
    userName() {
      let userName = ''
      if(!this.isGender) userName = 'Выберите пол'
      else userName = 'Физические показатели'
      return userName
    }
  },
  methods: {
    isInputNumber(event, value) {
      if (!/\d/.test(event.key) &&
          (event.key !== "." || /\./.test(value))
      )
        return event.preventDefault();
    },
    toPrevSection() {
      this.isGender = false
    },
    toUserForm() {
      this.isGender = true
    },
    getValue(evt) {
      this.radioBtn = evt
    },
  }
}
</script>

<style lang="scss" scoped>
.slide-fade-enter-active, .slide-fade-leave-active {
  transition: all .1s ease;
}
.slide-fade-enter, .slide-fade-leave-to {
  transform: translateX(10px);
  opacity: 0;
}
.home {
  display: flex;
  justify-content: center;
  align-items: center;
  &__user-block {

  }
}
.user {
  display: flex;
  flex-direction: column;
  //justify-content: space-around;
  justify-content: space-between;
  position: relative;
  max-width: 375px;
  min-width: 375px;
  min-height: 800px;
  border-radius: 40px;
  background: #2B2E3B;
  //padding: 0 20px;
  box-sizing: border-box;
  &.padding {
    padding: 0 39px;
  }
  &__header {
    height: 100px;
    //position: absolute;
    //top: 0;
    //left: 0;
    width: 100%;
    background: #292B38;
    border-radius: 40px 40px 0 0;
    padding: 14px 21px 23px;
    box-shadow: 4px 4px 9px #181A27, -4px -4px 13px rgba(121, 123, 136, 0.36);
    box-sizing: border-box;
  }
  &__admin {
    //margin-top: 100px;
    display: flex;
    justify-content: space-around;
    padding: 0 20px;
  }
  &__form {
    //margin-top: 100px;
    padding: 0 20px;
  }
  &__action {
    //margin-top: 94px;
    padding: 0 20px;
    margin-bottom: 44px;
  }
}
.header {
  &__time {
    font-size: 15px;
    line-height: 18px;
    text-align: justify;
    letter-spacing: 0.232836px;
    color: #FFFFFF;
  }
  &__action {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: center;
    margin-top: 20px;
    &.is-form {
      justify-content: flex-start;
    }
  }
  &__back-icon {

  }
  &__icon-button {
    background: linear-gradient(135deg, #1C1E2B 0%, #323441 100%);
    box-shadow: 2px 2px 10px #0A0C15, -2px -2px 10px rgba(255, 255, 255, 0.27);
    border-radius: 7px;
    width: 40px;
    height: 40px;
    margin-right: 10px;
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    &:hover {

    }
  }
  &__name {
    font-weight: normal;
    font-size: 23px;
    line-height: 27px;
    text-align: center;
    color: #C2C9D4;
  }
}
</style>
