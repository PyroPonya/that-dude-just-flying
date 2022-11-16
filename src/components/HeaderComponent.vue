<template>
  <div class="container__header">
    <div class="logo"></div>
    <div
      :style="selectorOpen ? '--rotate: -135deg' : '--rotate: 45deg'"
      @click="selectorOpen = !selectorOpen"
      class="container__lang"
    >
      <div
        :style="`background: url(${avLang[selectedLang]})`"
        class="lang__logo"
      ></div>
      <div class="lang__title">{{ selectedLang }}</div>
      <div v-if="selectorOpen" class="lang__dropdown">
        <div
          @click="setLanguage(id)"
          v-for="(el, id) in avLang"
          :key="id"
          class="dropdown__el"
        >
          <div
            :style="`background: url(${avLang[id]})`"
            class="lang__logo"
          ></div>
          <div class="lang__title">{{ id }}</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue';
import CA_svg from '/src/assets/header/CA.svg';
import EN_svg from '/src/assets/header/EN.svg';
import AU_svg from '/src/assets/header/AU.svg';
import NZ_svg from '/src/assets/header/NZ.svg';
import DE_svg from '/src/assets/header/DE.svg';
export default {
  props: ['store', 'currentLanguage'],
  setup(props, { emit }) {
    const selectorOpen = ref(false);
    const selectedLang = ref('EN');
    const avLang = {
      CA: CA_svg,
      EN: EN_svg,
      AU: AU_svg,
      NZ: NZ_svg,
      DE: DE_svg,
    };
    const setLanguage = (id) => {
      selectedLang.value = id;
      emit('setLang', selectedLang.value.toLowerCase());
    };
    const requestRedirect = (where) => {
      emit('requestRedirect', where);
    };
    return {
      selectorOpen,
      avLang,
      selectedLang,
      props,
      setLanguage,
      requestRedirect,
    };
  },
};
</script>

<style lang="sass" scoped>
$rotate: 45deg
:root
  --rotate: 45deg
.container__header
  // position: fixed
  // top: 0px
  // left: 0px
  display: flex
  flex-wrap: nowrap
  flex-direction: row
  align-items: flex-start
  justify-content: space-between
  width: 100%
  min-height: 135px
  // padding: 0 5%
  .logo
    width: 265px
    height: 134px
    background: url('/src/assets/header/logo.svg')
    background-position: center
    background-size: contain
    background-repeat: no-repeat
  .container__lang
    position: relative
    display: flex
    flex-direction: row
    justify-content: flex-start
    align-items: center
    gap: 15px
    padding: 10px 8px
    min-width: 130px
    height: 50px
    background: rgba(0, 0, 0, 0.6)
    border-radius: 10px
    cursor: pointer
    transition: all 0.3s ease-in-out
    .lang__logo
      background-position: center
      background-repeat: no-repeat
      height: 30px
      width: 50px
    .lang__title
      font-family: 'Montserrat'
      font-style: normal
      font-weight: 700
      font-size: 14px
      line-height: 114.7%
      color: #FFFFFF
      text-align: center
    &::after
      content: ''
      position: absolute
      height: 10px
      width: 10px
      border-right: 2px solid #ffffff
      border-bottom: 2px solid #ffffff
      right: 10%
      bottom: 45%
      transform: rotate(var(--rotate))
      transition: all 0.3s ease-in-out
    .lang__dropdown
      z-index: 122
      position: absolute
      display: flex
      flex-direction: column
      align-items: flex-start
      justify-content: center
      gap: 10px
      padding: 14px 8px
      min-width: 130px
      max-width: 130px
      top: 100%
      // left: 10%
      left: 0%
      border-radius: 10px
      background: rgba(0, 0, 0, 0.6)
      .dropdown__el
        cursor: pointer
        display: flex
        flex-direction: row
        justify-content: flex-start
        align-items: center
        gap: 15px
        min-width: 130px
        width: 100%
        height: 50px
        color: #FFFFFF
@media (max-width: 1010px)
  .container__header
    align-items: center
@media (max-width: 750px)
  .container__header
    max-height: 50px
    min-height: 50px
    .logo
      height: 50px
      width: 50px
      background: url('/src/assets/header/logo_mobile.svg')
      background-position: center
      background-size: contain
      background-repeat: no-repeat
</style>
