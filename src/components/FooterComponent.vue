<template>
  <div :class="isMobile ? 'foo__mobile' : ''" class="container__footer">
    <div class="footer__title">
      {{ store.languages[currentLanguage].interface.landing.footer.title }}
    </div>
    <div class="footer__bg">
      <div
        v-for="(el, id) in store.languages[currentLanguage].interface.landing
          .footer.steps"
        :key="id"
        :class="activeStep == id ? 'bg__element-active' : ''"
        class="bg__element"
      >
        <div class="element__num">{{ id + 1 }}</div>
        <div class="element__text">
          {{
            store.languages[currentLanguage].interface.landing.footer.steps[id]
          }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['store', 'currentLanguage', 'activeStep', 'isMobile'],
  setup(props) {
    return {
      props,
    };
  },
};
</script>

<style lang="sass" scoped>
.container__footer
  min-height: 150px
  width: 100%
  display: flex
  flex-direction: column
  gap: 25px
  .footer__title
    font-weight: 600
    font-size: 30px
    line-height: 37px
    letter-spacing: 0.01em
    text-transform: uppercase
    color: #B9C6D6
    text-align: left
  .footer__bg
    display: flex
    flex-direction: row
    align-items: center
    justify-content: space-between
    width: 100%
    min-height: 90px
    background: rgba(0, 0, 0, 0.54)
    border-radius: 500px
    .bg__element
      max-width: 335px
      min-width: 150px
      min-height: 90px
      display: flex
      flex-direction: row
      align-items: center
      gap: 25px
      .element__num
        display: flex
        align-items: center
        justify-content: center
        background: #13171E
        font-weight: 900
        font-size: 41.2844px
        line-height: 50px
        letter-spacing: 0.01em
        text-transform: uppercase
        color: #B9C6D6
        min-height: 90px
        min-width: 90px
        max-height: 90px
        max-width: 90px
        border-radius: 50%
        border: 1.65px solid #B9C6D6
      .element__text
        display: flex
        align-items: center
        justify-content: center
        max-width: 220px
        text-transform: uppercase
        font-weight: 600
        font-size: 22px
        line-height: 27px
        letter-spacing: 0.01em
        color: #B9C6D6
      &-active
        .element__num
          color: #E49100
          border: 1.65px solid #E49100
        .element__text
          color: #E49100
@media (width < 1010px)
  .container__footer
    padding-top: 130px
    .footer__title
      display: none
    .footer__bg
      .bg__element
        min-height: 70px
        .element__num
          min-height: 70px
          min-width: 70px
          max-height: 70px
          max-width: 70px
          font-size: 32px
          line-height: 39px
        .element__text
          font-size: 20px
          line-height: 24px
          max-width: 150px
          max-height: 50px
@media (width < 750px)
  .container__footer
    padding-top: 130px
    .footer__title
      display: none
    .footer__bg
      flex-direction: column
      background: none
      gap: 18px
      .bg__element
        min-width: 240px
        max-width: 240px
        min-height: 40px
        background: rgba(0, 0, 0, 0.54)
        border-radius: 30px
        gap: 15px
        .element__num
          font-size: 18.3486px
          line-height: 22px
          min-height: 40px
          min-width: 40px
          max-height: 40px
          max-width: 40px
        .element__text
          font-size: 16px
          line-height: 20px
          font-weight: 600
          font-size: 16px
          line-height: 20px
          letter-spacing: 0.01em
          max-width: 153px
          // text-align: center
</style>
