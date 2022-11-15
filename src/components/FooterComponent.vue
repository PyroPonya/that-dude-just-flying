<template>
  <div class="container__footer">
    <div class="footer__title">
      {{ store.languages[currentLanguage].interface.landing.footer.title }}
    </div>
    <div class="footer__bg">
      <div
        v-for="(el, id) in store.languages[currentLanguage].interface.landing
          .footer.steps"
        :key="id"
        class="bg__element"
      >
        <div class="element__num">{{ id + 1 }}</div>
        <div class="element__text">Registrieren Sie sich auf der Website</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['store', 'currentLanguage'],
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
      min-width: 335px
      min-height: 90px
      display: flex
      flex-direction: row
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
</style>
