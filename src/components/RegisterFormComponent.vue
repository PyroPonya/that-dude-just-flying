<template>
  <div class="form">
    <div class="content">
      <div class="form__title">
        {{ store.languages[currentLanguage].interface.register.welcome }}
      </div>
      <div :class="errorMail ? 'form__error-mail' : ''" class="mail-container">
        <input
          v-model="dataBlob.mail"
          :class="errorMail ? 'form__input-error' : ''"
          class="form__mail form__input"
          :placeholder="
            store.languages[currentLanguage].interface.register.e_mail
          "
        />
      </div>
      <div
        :class="errorPassword ? 'form__error-password' : ''"
        class="pass-container"
      >
        <input
          v-model="dataBlob.password"
          :type="
            displayPassword
              ? (passwordFieldType = 'text')
              : (passwordFieldType = 'password')
          "
          class="form__password form__input"
          placeholder="Password"
        />
        <div
          @click="displayPassword = !displayPassword"
          class="form__password-toggle"
        ></div>
      </div>
      <div
        @click="
          showCurrency = !showCurrency;
          showCountry = false;
        "
        :style="showCurrency ? '--rotate: 45deg' : '--rotate: -135deg'"
        class="form__currency form__input form__input-select"
      >
        {{ !dataBlob.currency ? 'Currency' : dataBlob.currency }}
        <div v-if="showCurrency" class="form__currency-dropdown dropdown">
          <div
            v-for="(el, id) in currencyArr"
            :key="id"
            class="dropdown__element"
            @click="dataBlob.currency = el"
          >
            {{ el }}
          </div>
        </div>
      </div>
      <div
        @click="
          showCountry = !showCountry;
          showCurrency = false;
        "
        :style="showCountry ? '--rotate: 45deg' : '--rotate: -135deg'"
        class="form__country form__input form__input-select"
      >
        {{ !dataBlob.country ? 'Country' : dataBlob.country }}
        <div v-if="showCountry" class="form__country-dropdown dropdown">
          <div
            v-for="(el, id) in countryList"
            :key="id"
            class="dropdown__element"
            @click="dataBlob.country = el"
          >
            {{ el }}
          </div>
        </div>
      </div>
      <div class="form__text conditions">
        <div
          class="checkbox"
          :class="dataBlob.termsChecked ? 'checkbox-checked' : ''"
          @click="dataBlob.termsChecked = !dataBlob.termsChecked"
        ></div>
        <div class="terms__text">
          {{ store.languages[currentLanguage].interface.register.terms[0] }}
          <a
            @click="requestRedirect(store.links.privacy_policy)"
            class="link"
            >{{
              store.languages[currentLanguage].interface.register.terms[1]
            }}</a
          >
          {{ store.languages[currentLanguage].interface.register.terms[2] }}
          <a
            @click="requestRedirect(store.links.terms)"
            class="link link__terms"
            >{{
              store.languages[currentLanguage].interface.register.terms[3]
            }}</a
          >
        </div>
      </div>
      <div class="form__text promos">
        <div
          class="checkbox"
          :class="dataBlob.promosChecked ? 'checkbox-checked' : ''"
          @click="dataBlob.promosChecked = !dataBlob.promosChecked"
        ></div>
        <div class="terms__text">
          {{ store.languages[currentLanguage].interface.register.promos }}
        </div>
      </div>
      <div @click="pushData" class="btn-container">
        <div class="form__btn">
          <div class="btn__text">
            {{ store.languages[currentLanguage].interface.register.sign_up }}
          </div>
        </div>
      </div>
      <div class="form__login">
        <div class="login__title">
          {{ store.languages[currentLanguage].interface.register.already }}
        </div>
        <div
          @click="requestRedirect(store.links.sign_in)"
          class="login__link link"
        >
          {{ store.languages[currentLanguage].interface.register.sign_in }}
        </div>
      </div>
    </div>
    <div class="form__partners">
      <div v-for="el in 10" :key="el" class="form__partners-element"></div>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue';
export default {
  props: ['store', 'currentLanguage'],
  setup(props, { emit }) {
    const termsChecked = ref(false);
    const promosChecked = ref(false);
    const showCurrency = ref(false);
    const errorMail = ref(false);
    const errorPassword = ref(false);
    const displayPassword = ref(true);
    const showCountry = ref(false);
    const formIsValid = ref(false);
    const currencyArr = [
      'EUR',
      'NZD',
      'AUD',
      'USD',
      'CAD',
      'NOK',
      'INR',
      'BTC',
      'BCH',
      'DOG',
      'ETH',
      'LTC',
      'USDT',
      'XRP',
      'TRX',
      'BNB',
    ];
    const countryList = [
      'Afghanistan',
      'Albania',
      'Algeria',
      'Andorra',
      'Angola',
      'Anguilla',
      'Antigua & Barbuda',
      'Argentina',
      'Armenia',
      'Aruba',
      'Australia',
      'Austria',
      'Azerbaijan',
      'Bahamas',
      'Bahrain',
      'Bangladesh',
      'Barbados',
      'Belarus',
      'Belgium',
      'Belize',
      'Benin',
      'Bermuda',
      'Bhutan',
      'Bolivia',
      'Bosnia & Herzegovina',
      'Botswana',
      'Brazil',
      'British Virgin Islands',
      'Brunei',
      'Bulgaria',
      'Burkina Faso',
      'Burundi',
      'Cambodia',
      'Cameroon',
      'Cape Verde',
      'Cayman Islands',
      'Chad',
      'Chile',
      'China',
      'Colombia',
      'Congo',
      'Cook Islands',
      'Costa Rica',
      'Cote D Ivoire',
      'Croatia',
      'Cruise Ship',
      'Cuba',
      'Cyprus',
      'Czech Republic',
      'Denmark',
      'Djibouti',
      'Dominica',
      'Dominican Republic',
      'Ecuador',
      'Egypt',
      'El Salvador',
      'Equatorial Guinea',
      'Estonia',
      'Ethiopia',
      'Falkland Islands',
      'Faroe Islands',
      'Fiji',
      'Finland',
      'France',
      'French Polynesia',
      'French West Indies',
      'Gabon',
      'Gambia',
      'Georgia',
      'Germany',
      'Ghana',
      'Gibraltar',
      'Greece',
      'Greenland',
      'Grenada',
      'Guam',
      'Guatemala',
      'Guernsey',
      'Guinea',
      'Guinea Bissau',
      'Guyana',
      'Haiti',
      'Honduras',
      'Hong Kong',
      'Hungary',
      'Iceland',
      'India',
      'Indonesia',
      'Iran',
      'Iraq',
      'Ireland',
      'Isle of Man',
      'Israel',
      'Italy',
      'Jamaica',
      'Japan',
      'Jersey',
      'Jordan',
      'Kazakhstan',
      'Kenya',
      'Kuwait',
      'Kyrgyz Republic',
      'Laos',
      'Latvia',
      'Lebanon',
      'Lesotho',
      'Liberia',
      'Libya',
      'Liechtenstein',
      'Lithuania',
      'Luxembourg',
      'Macau',
      'Macedonia',
      'Madagascar',
      'Malawi',
      'Malaysia',
      'Maldives',
      'Mali',
      'Malta',
      'Mauritania',
      'Mauritius',
      'Mexico',
      'Moldova',
      'Monaco',
      'Mongolia',
      'Montenegro',
      'Montserrat',
      'Morocco',
      'Mozambique',
      'Namibia',
      'Nepal',
      'Netherlands',
      'Netherlands Antilles',
      'New Caledonia',
      'New Zealand',
      'Nicaragua',
      'Niger',
      'Nigeria',
      'Norway',
      'Oman',
      'Pakistan',
      'Palestine',
      'Panama',
      'Papua New Guinea',
      'Paraguay',
      'Peru',
      'Philippines',
      'Poland',
      'Portugal',
      'Puerto Rico',
      'Qatar',
      'Reunion',
      'Romania',
      'Russia',
      'Rwanda',
      'Saint Pierre & Miquelon',
      'Samoa',
      'San Marino',
      'Satellite',
      'Saudi Arabia',
      'Senegal',
      'Serbia',
      'Seychelles',
      'Sierra Leone',
      'Singapore',
      'Slovakia',
      'Slovenia',
      'South Africa',
      'South Korea',
      'Spain',
      'Sri Lanka',
      'St Kitts & Nevis',
      'St Lucia',
      'St Vincent',
      'St. Lucia',
      'Sudan',
      'Suriname',
      'Swaziland',
      'Sweden',
      'Switzerland',
      'Syria',
      'Taiwan',
      'Tajikistan',
      'Tanzania',
      'Thailand',
      "Timor L'Este",
      'Togo',
      'Tonga',
      'Trinidad & Tobago',
      'Tunisia',
      'Turkey',
      'Turkmenistan',
      'Turks & Caicos',
      'Uganda',
      'Ukraine',
      'United Arab Emirates',
      'United Kingdom',
      'Uruguay',
      'Uzbekistan',
      'Venezuela',
      'Vietnam',
      'Virgin Islands (US)',
      'Yemen',
      'Zambia',
      'Zimbabwe',
    ];
    const countryArr = [];
    const dataBlob = ref({
      mail: '',
      password: '',
      currency: '',
      country: '',
      termsChecked: false,
      promosChecked: false,
    });
    // validate data
    const validateData = () => {
      let errorCounter = 0;
      // mail
      if (!dataBlob.value.mail.slice('').includes('@')) {
        errorMail.value = true;
        // return 'error';
        errorCounter++;
      } else {
        errorMail.value = false;
      }
      // pass
      if (dataBlob.value.password.length < 8) {
        errorPassword.value = true;
        // return 'error';
        errorCounter++;
      } else {
        errorPassword.value = false;
      }
      if (!dataBlob.value.currency || !dataBlob.value.country) {
        errorCounter++;
      }
      if (!dataBlob.value.termsChecked) {
        errorCounter++;
      }
      if (errorCounter > 0) {
        formIsValid.value = false;
        return false;
      } else {
        formIsValid.value = true;
        return true;
      }
    };
    const requestRedirect = (where) => {
      emit('requestRedirect', where);
    };
    // emits registration data
    const pushData = () => {
      if (validateData()) {
        emit('regData', dataBlob.value);
        dataBlob.value = {
          mail: '',
          password: '',
          currency: '',
          country: '',
          termsChecked: false,
          promosChecked: false,
        };
      } else {
        return false;
      }
    };
    // ////////////////////////////
    // watchEffect(() => {
    //   // console.log(dataBlob.value);
    //   console.log('mail: ', dataBlob.value.mail);
    //   const valid = validateData();
    //   console.log(valid);
    //   // console.log('pass: ', dataBlob.value.password);
    //   // console.log('terms: ', dataBlob.value.termsChecked);
    //   // console.log('promos: ', dataBlob.value.promosChecked);
    // });
    // ///////////////////////////
    return {
      termsChecked,
      promosChecked,
      dataBlob,
      currencyArr,
      countryArr,
      showCountry,
      showCurrency,
      errorMail,
      errorPassword,
      displayPassword,
      countryList,
      formIsValid,
      props,
      validateData,
      pushData,
      requestRedirect,
    };
  },
};
</script>

<style lang="sass" scoped>
:root
  --rotate: -135deg //45deg
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
.dropdown
  position: relative
  top: 100% + 5
  left: 0
  display: grid
  grid-template: 1fr 1fr 1fr 1fr / 1fr 1fr 1fr 1fr
  padding: 6px 12px
  width: 300px
  background-color: #0E1219
  border-bottom-left-radius: 12px
  border-bottom-right-radius: 12px
  z-index: 111
  // prevent selection start
  user-select: none
  -webkit-user-select: none
  -moz-user-select: none
  -khtml-user-select: none
  -ms-user-select: none
  // prevent selection end
  &__element
    // margin: 6px 10px
    display: flex
    align-items: center
    justify-content: center
    height: 25px
    width: 50px
    &:hover
      background: linear-gradient(256.33deg, #FFB639 18.19%, #E49100 80.14%)
      border-radius: 6px
      color: #1D232C
.form
  background: #2B3446
  border-radius: 20px
  padding: 25px
  width: 400px
  min-height: 550px
  display: flex
  flex-direction: column
  &__error
    &-mail::after
      content: 'Email address must contain the "@" symbol'
      text-transform: uppercase
      height: 100%
      width: 100%
      font-family: 'Montserrat'
      font-style: normal
      font-weight: 600
      font-size: 12px
      line-height: 15px
      display: flex
      align-items: center
      letter-spacing: 0.01em
      color: #FF2525
      margin: 5px
    &-password::after
      content: 'IS TOO SHORT (MINIMUM IS 8 CHARACTERS)'
      text-transform: uppercase
      height: 100%
      width: 100%
      font-family: 'Montserrat'
      font-style: normal
      font-weight: 600
      font-size: 12px
      line-height: 15px
      display: flex
      align-items: center
      letter-spacing: 0.01em
      color: #FF2525
      margin: 5px
  .content
    padding: 25px
    padding-top: 0
  &__title
    display: flex
    justify-content: flex-start
    font-family: 'Montserrat'
    font-style: normal
    font-weight: 900
    font-size: 28px
    line-height: 34px
    text-align: center
    color: #FFFFFF
    margin-bottom: 14px
    text-transform: uppercase
  &__input
    background: #1C2330
    border-radius: 12px
    display: flex
    align-items: center
    justify-content: flex-start
    font-family: 'Montserrat'
    font-style: normal
    font-weight: 600
    font-size: 14px
    line-height: 17px
    letter-spacing: 0.01em
    background: #1C2330
    border: none
    outline: none
    border-radius: 12px
    height: 50px
    width: 300px
    margin-bottom: 6px
    padding: 0 20px
    color: #FFFFFF
    &::placeholder
      color: #657083
      text-transform: capitalize
    &-select
      position: relative
      transition: all 3s ease-in-out
      cursor: pointer
      &::after
        position: absolute
        content: ''
        width: 8px
        height: 8px
        border-top: 2px solid #657083
        border-left: 2px solid #657083
        right: 5%
        top: 45%
        transform: rotate(var(--rotate))
        transition: all 0.3s ease-in-out
    &-error
      outline: 1px solid #E49100
      border-radius: 12px
  &__mail
  .pass-container
    position: relative
  &__password
    &-toggle
      position: absolute
      height: 10px
      width: 15px
      right: 5%
      top: 20px
      background-image: url('/src/assets/form/grey-eye.svg')
      cursor: pointer
      &:hover
        filter: invert(92%) sepia(200%) saturate(20%) hue-rotate(2000deg) brightness(89%) contrast(200%)
  &__currency
    position: relative
    color: #FFFFFF
    &-dropdown
      position: absolute
  &__country
    position: relative
    color: #FFFFFF
    &-dropdown
      position: absolute
      display: flex
      flex-direction: column
      align-items: center
      justify-content: flex-start
      gap: 10px
      max-height: 200px
      overflow-y: scroll
      .dropdown__element
        // margin: 6px 10px
        display: flex
        align-items: center
        justify-content: center
        padding: 15px
        width: 100%
        &:hover
          background: linear-gradient(256.33deg, #FFB639 18.19%, #E49100 80.14%)
          border-radius: 6px
          color: #1D232C
  &__text
    display: flex
    flex-direction: row
    align-items: center
    justify-content: flex-start
    gap: 8px
    margin: 10px 0px
    .checkbox
      border: 1px solid #B9C6D6
      outline: 1px solid #B9C6D6
      border-radius: 5px
      min-height: 20px
      min-width: 20px
      cursor: pointer
      &-checked
        border: 2px solid #2B3446
        border-radius: 2px
        min-height: 20px
        min-width: 20px
        position: relative
        background: #B9C6D6
        outline: 2px solid #B9C6D6
    .terms__text
      font-family: 'Montserrat'
      font-style: normal
      font-weight: 600
      font-size: 12px
      line-height: 15px
      align-items: center
      letter-spacing: 0.01em
      color: #B9C6D6
  &__mailing
  .btn-container
    background-color: #13171E
    border-radius: 12px
    width: 100%
    height: 50px
    margin: 14px 0 7px 0
    // prevent selection start
    user-select: none
    -webkit-user-select: none
    -moz-user-select: none
    -khtml-user-select: none
    -ms-user-select: none
    // prevent selection end
  &__btn
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
      font-size: 18px
      line-height: 22px
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

  &__login
    display: flex
    gap: 9px
    justify-content: center
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
  &__partners
    display: flex
    flex-direction: row
    align-items: center
    justify-content: center
    flex-wrap: wrap
    min-width: 100%
    gap: 9px
    &-element
      // margin: 10px 8px
      &:nth-of-type(1)
        height: 24px
        width: 30px
        background: center / contain no-repeat url("/src/assets/form/maestro.svg")
      &:nth-of-type(2)
        height: 24px
        width: 31px
        background: center / contain no-repeat url("/src/assets/form/mastercard.svg")
      &:nth-of-type(3)
        height: 24px
        width: 55px
        background: center / contain no-repeat url("/src/assets/form/visa.svg")
      &:nth-of-type(4)
        height: 24px
        width: 47px
        background: center / contain no-repeat url("/src/assets/form/interac-transfer.svg")
      &:nth-of-type(5)
        height: 24px
        width: 69px
        background: center / contain no-repeat url("/src/assets/form/neosurf.svg")
        // filtering from pink to gray
        filter: invert(92%) sepia(200%) saturate(20%) hue-rotate(2000deg) brightness(89%) contrast(200%)
      &:nth-of-type(6)
        height: 24px
        width: 61px
        background: center / contain no-repeat url("/src/assets/form/flexepin.svg")
      &:nth-of-type(7)
        height: 24px
        width: 69px
        background: center / contain no-repeat url("/src/assets/form/mifinity.svg")
      &:nth-of-type(8)
        height: 24px
        width: 54px
        background: center / contain no-repeat url("/src/assets/form/bank-transfer.svg")
      &:nth-of-type(9)
        height: 24px
        width: 69px
        background: center / contain no-repeat url("/src/assets/form/payz.svg")
      &:nth-of-type(10)
        height: 24px
        width: 38px
        background: center / contain no-repeat url("/src/assets/form/iDebit.svg")

// @media (max-width: 415px)
//   .form
//     display: flex !important
//     flex-direction: column
//     justify-content: center
//     align-items: center
//     max-width: 330px
//     padding: 20px 40px
//     .content
//       padding: 0px 0px 15px 0px
//       .mail__container, .pass__container, .form__input, .form__btn, .btn-container
//         min-width: 20px
//         max-width: 240px
//       .form__password-toggle
//         right: 10%
//       .form__login
//         justify-content: flex-start
//         align-items: flex-start
//         gap: 5px
//       .dropdown
//         max-width: 240px
@media (max-width: 750px)
  .form
    max-width: 330px
    display: flex !important
    justify-content: center
    align-items: center
    .content
      display: flex
      flex-direction: column
      justify-content: center
      align-items: flex-start
      max-width: 242px
      padding: 0
      .mail__container, .pass__container, .form__input, .form__btn, .btn-container
        max-width: 240px
      .form__login
        gap: 5px
        margin-bottom: 15px
    .form__partners
      padding: 0px 5px
</style>
