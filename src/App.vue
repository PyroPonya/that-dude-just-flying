<template>
  <div class="main__container">
    <div class="container">
      <HeaderComponent
        class="header"
        :store="store"
        @setLang="(payload) => updateLanguage(payload)"
        @requestRedirect="(payload) => redirectTo(payload)"
      />
      <div class="container__body">
        <div class="container__text">
          <div class="text__title">
            {{ store.languages[currentLanguage].interface.landing.title }}
          </div>
          <div class="text__body">
            {{ store.languages[currentLanguage].interface.landing.body }}
          </div>
          <FooterComponent
            v-if="isMobile"
            :store="store"
            :currentLanguage="currentLanguage"
            :activeStep="activeStep"
            :isMobile="isMobile"
            class="footer footer__mobile"
          />
          <div
            @click="redirectTo(store.links.sportsbook)"
            class="btn-container"
          >
            <div class="form__btn">
              <div class="btn__text">
                {{
                  store.languages[currentLanguage].interface.register.sign_up
                }}
              </div>
            </div>
          </div>
          <div class="form__login">
            <div class="login__title">
              {{ store.languages[currentLanguage].interface.register.already }}
            </div>
            <a>
              <div
                @click="redirectTo(store.links.sign_in)"
                class="login__link link"
              >
                {{
                  store.languages[currentLanguage].interface.register.sign_in
                }}
              </div>
            </a>
          </div>
        </div>
        <!-- <register-form-component
          class="register"
          :store="store"
          :currentLanguage="currentLanguage"
          :style="registerFormDisplay ? 'display: block' : 'display:none'"
          @requestRedirect="(payload) => redirectTo(payload)"
          @regData="(payload) => apiRegisterData(payload)"
        /> -->
      </div>
      <FooterComponent
        v-if="!isMobile"
        :store="store"
        :currentLanguage="currentLanguage"
        :activeStep="activeStep"
        :isMobile="isMobile"
        class="footer footer__main"
      />
    </div>
  </div>
</template>

<script setup>
// import RegisterFormComponent from './components/RegisterFormComponent.vue';
import HeaderComponent from './components/HeaderComponent.vue';
import FooterComponent from './components/FooterComponent.vue';
import { onMounted, onUnmounted, ref } from 'vue';
import useStore from './Store/store';
const store = useStore;
const activeStep = ref(0);
const isMobile = window.innerWidth <= 750 ? true : false;
// const registerFormDisplay = ref(true);
// steps animatiom start
function intervalId(duration = 2000) {
  setInterval(() => {
    activeStep.value++;
    activeStep.value > 2 ? (activeStep.value = 0) : '';
  }, duration);
}
onMounted(() => {
  intervalId(2000);
});
onUnmounted(() => {
  clearInterval(intervalId());
});
// steps animation end
// blurify start
const scrolly = ref();
const blur = ref('none');
const currentLanguage = ref('en');
const watchScroll = () => {
  scrolly.value = window.top.scrollY;
  scrolly.value > 60 ? (blur.value = 'blur(7.5px)') : (blur.value = '');
};
onMounted(() => {
  document.addEventListener('scroll', (e) => watchScroll(e));
});
onUnmounted(() => {
  document.removeEventListener('scroll', watchScroll());
});
// blurify end
const redirectTo = (where) => {
  window.location.assign(where);
};
// const apiRegisterData = (proxyData) => {
//   console.log(proxyData);
// };
const updateLanguage = (lang) => {
  currentLanguage.value = lang;
  console.log('selectedLang: ', lang);
};
</script>

<style lang="sass" scoped>
.main__container
  position: relative
  min-height: 100vh
  width: 100vw
  display: flex
  align-items: center
  justify-content: center
  background-color: black
  background: url('./assets/bg_main.jpg')
  background-position: center
  background-size: cover
  background-repeat: no-repeat
  // padding:
  .container
    max-width: 1300px
    width: 100%
    height: 100%
    display: flex
    flex-direction: column
    align-items: center
    justify-content: center
    .header
      z-index: 2
      width: 100%
    .container__body
      width: 100%
      min-height: 500px
      display: flex
      flex-direction: row
      align-items: center
      justify-content: space-between
      .container__text
        display: flex
        flex-direction: column
        font-family: 'Montserrat'
        font-style: normal
        max-width: 685px
        gap: 5px
        .btn-container
          background-color: #13171E
          border-radius: 12px
          width: 100%
          max-width: 320px
          height: 50px
          margin: 14px 0 7px 0
          // prevent selection start
          user-select: none
          -webkit-user-select: none
          -moz-user-select: none
          -khtml-user-select: none
          -ms-user-select: none
          // prevent selection end
          .form__btn
            display: flex
            flex-direction: row
            justify-content: center
            align-items: center
            min-width: 100%
            min-height: 100%
            gap: 10px
            background: linear-gradient(256.33deg, #FFB639 18.19%, #E49100 80.14%)
            color: #13171E
            box-shadow: 0px 4px 6px rgba(0, 0, 0, 0.25)
            border-radius: 12px
            cursor: pointer
            text-transform: uppercase
            &-error
              display: flex
              flex-direction: row
              justify-content: center
              align-items: center
              min-width: 300px
              min-height: 50px
              margin: 14px 0 7px 0
              gap: 10px
              background-color: rgba(0, 0, 0, 0.25)
              color: rgba(228, 145, 0, 0.6)
              box-shadow: 0px 4px 6px rgba(0, 0, 0, 0.25)
              border-radius: 12px
              cursor: not-allowed
            .btn__text
              font-family: 'Montserrat'
              font-style: normal
              font-weight: 700
              font-size: 30px
              line-height: 37px
              letter-spacing: 0.01em
              color: #1D232C
            &:hover
              background: linear-gradient(256.33deg, #FFD644 18.19%, #FFBB0E 80.14%)
            &:active
              background: linear-gradient(256.33deg, #FFB639 18.19%, #E49100 80.14%)
              -webkit-background-clip: text
              -webkit-text-fill-color: transparent
              background-clip: text
              text-fill-color: transparent
        .form__login
          display: flex
          gap: 9px
          max-width: 320px
          justify-content: center
          white-space: nowrap
          .login__title
            font-family: 'Montserrat'
            font-style: normal
            font-weight: 400
            font-size: 14px
            line-height: 17px
            letter-spacing: 0.01em
            color: #B9C6D6
          .login__link
            font-family: 'Montserrat'
            font-style: normal
            font-weight: 700
            font-size: 14px
            line-height: 17px
            text-decoration: underline
            text-transform: capitalize
        .link
          background: linear-gradient(256.33deg, #FFB639 18.19%, #E49100 80.14%)
          background-clip: text
          text-fill-color: transparent
          -webkit-background-clip: text
          -webkit-text-fill-color: transparent
          cursor: pointer
          border-bottom: 1px solid #FFB639
          margin-bottom: -1px
          &:hover
            background: linear-gradient(256.33deg, #FFD644 18.19%, #FFBB0E 80.14%)
            background-clip: text
            text-fill-color: transparent
            -webkit-background-clip: text
            -webkit-text-fill-color: transparent
            border-bottom: 1px solid #FFD644
            margin-bottom: -1px
          a
            text-decoration: none
          &__terms
            position: relative
            &::after
              content: '*'
        .text__title
          font-weight: 600
          font-size: 30px
          line-height: 37px
          letter-spacing: 0.01em
          text-transform: uppercase
          color: #B9C6D6
        .text__body
          font-weight: 900
          font-size: 40px
          line-height: 49px
          letter-spacing: 0.01em
          text-transform: uppercase
          color: #FFFFFF
      .register
        align-self: flex-end
@media (max-width: 1010px)
  .main__container
    background-position: right
    .container
      padding: 30px 50px 20px 50px
      .container__footer
        padding-top: 5%
      .container__body
        // height: 100vh
        gap: 20px
        align-items: flex-start
        padding-top: 80px
        .container__text
          max-width: 425px
          gap: 0px
        .footer
          bottom: 0
          .text__title
            font-size: 24px
            line-height: 29px
          .text__body
            font-size: 30px
            line-height: 37px
@media (max-width: 750px)
  .main__container
    background: url('./assets/bg_mobile.jpg')
    background-position: center
    background-size: cover
    background-repeat: no-repeat
    background-position: top -20%
    min-width: 400px
    .container
      padding: 10px 15px
      gap: 15px
      .header
      .container__body
        flex-direction: column
        // justify-content: center
        align-items: center
        gap: 0px
        padding-top: 0
        .container__footer
          padding-top: 130%
        .container__text
          display: flex
          align-items: center
          max-width: 210px
          text-align: center
          height: 100%
          .text__title
            margin-bottom: 10px
          .btn-container
            .form__btn
              .btn__text
                font-size: 18px
                line-height: 22px
          .footer__mobile
            padding-bottom: 30px
            .footer__bg
              width: 240px
          .text__title
            font-size: 14px
            line-height: 17px
          .text__body
            font-size: 20px
            line-height: 24px
            min-width: 400px
            font-size: 30px
            line-height: 30px
        .register
          align-self: center
        // .footer__mobile
        //   .footer__bg
        //     display: flex
        //     flex-direction: column
</style>
