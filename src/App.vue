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
        <register-form-component
          class="register"
          :store="store"
          :currentLanguage="currentLanguage"
          :style="registerFormDisplay ? 'display: block' : 'display:none'"
          @requestRedirect="(payload) => redirectTo(payload)"
          @regData="(payload) => apiRegisterData(payload)"
        />
      </div>
      <FooterComponent :store="store" :currentLanguage="currentLanguage" />
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
// const isMobile = window.innerWidth <= 415 ? true : false;
const registerFormDisplay = ref(true);
// blurify start
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
</style>
