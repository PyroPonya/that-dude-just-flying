<template>
  <div class="main__container">
    <div class="container">
      <HeaderComponent
        class="header"
        @setLang="(payload) => updateLanguage(payload)"
      />
      <div class="container__body">
        <div class="container__text">
          <div class="text__title">
            {{ store.languages[currentLanguage].interface.landing.title }}
          </div>
          <div class="text__body">
            {{ store.languages[currentLanguage].interface.landing.body }}
          </div>
        </div>
        <FooterComponent
          v-if="isMobile"
          :store="store"
          :currentLanguage="currentLanguage"
          :activeStep="activeStep"
          :isMobile="isMobile"
          class="footer footer__mobile"
        />
        <register-form-component
          class="register"
          :store="store"
          :currentLanguage="currentLanguage"
          :style="registerFormDisplay ? 'display: block' : 'display:none'"
          @requestRedirect="(payload) => redirectTo(payload)"
          @regData="(payload) => apiRegisterData(payload)"
        />
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
import RegisterFormComponent from './components/RegisterFormComponent.vue';
import HeaderComponent from './components/HeaderComponent.vue';
import FooterComponent from './components/FooterComponent.vue';
import { onMounted, onUnmounted, ref } from 'vue';
import useStore from './Store/store';
const store = useStore;
const activeStep = ref(0);
const isMobile = window.innerWidth <= 750 ? true : false;
const registerFormDisplay = ref(true);
// blurify start
// steps animatiom start
function intervalId(duration = 3000) {
  setInterval(() => {
    activeStep.value++;
    activeStep.value > 2 ? (activeStep.value = 0) : '';
  }, duration);
}
onMounted(() => {
  intervalId(3000);
});
onUnmounted(() => {
  clearInterval(intervalId());
});
// steps animation end
const scrolly = ref();
const blur = ref('none');
const currentLanguage = ref('en');
const watchScroll = () => {
  scrolly.value = window.top.scrollY;
  scrolly.value > 60 ? (blur.value = 'blur(7.5px)') : (blur.value = '');
};
// const checkScreen = () => {
//   window.innerWidth <= 415 ? store.useForm() : '';
// };
onMounted(() => {
  document.addEventListener('scroll', (e) => watchScroll(e));
  // checkScreen();
});
onUnmounted(() => {
  document.removeEventListener('scroll', watchScroll());
});
// blurify end
const redirectTo = (where) => {
  window.location.assign(where);
};
const apiRegisterData = (proxyData) => {
  console.log(proxyData);
};
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
@media (width < 1010px)
  .main__container
    .container
      padding: 30px 50px 120px 50px
      .container__body
        gap: 20px
        align-items: flex-start
        padding-top: 80px
        .container__text
          max-width: 425px
          gap: 20px
          .text__title
            font-size: 24px
            line-height: 29px
          .text__body
            font-size: 30px
            line-height: 37px
@media (width < 750px)
  .main__container
    background: url('./assets/bg_mobile.jpg')
    background-position: center
    background-size: cover
    background-repeat: no-repeat
    .container
      padding: 10px 15px
      gap: 15px
      .header
      .container__body
        flex-direction: column
        justify-content: center
        align-items: center
        gap: 30px
        padding-top: 0
        .container__text
          max-width: 210px
          text-align: center
          text-justify: center
          .text__title
            font-size: 14px
            line-height: 17px
          .text__body
            font-size: 20px
            line-height: 24px
        .register
          align-self: center
        // .footer__mobile
        //   .footer__bg
        //     display: flex
        //     flex-direction: column
</style>
