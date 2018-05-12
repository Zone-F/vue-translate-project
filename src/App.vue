<template>
  <div id="app">
    <h2>简单翻译</h2><span>简单/易用/便捷</span>
    <TranslateForm v-on:formSubmit="textTranslate"></TranslateForm>
    <TranslateText :translated-text="translatedText"></TranslateText>
  </div>
</template>

<script>
import TranslateForm from './components/TranslateForm.vue'
import TranslateText from './components/TranslateText.vue'
import md5 from 'blueimp-md5'
import $ from 'jquery'

export default {
  name: 'App',
  data: function () {
    return {
      translatedText: '2',
      appKey: '47bb6e424790df89',
      key: 'NH2VxBadIlKlT2b2qjxaSu221dSC78Ew',
      salt: (new Date()).getTime(),
      from: '',
      to: 'en'
    }
  },
  components: {
    TranslateForm, TranslateText
  },
  methods: {
    textTranslate: function (text, to) {
      let vm = this
      $.ajax({
        url: 'http://openapi.youdao.com/api',
        type: 'post',
        dataType: 'jsonp',
        data: {
          q: text,
          appKey: this.appKey,
          salt: this.salt,
          from: this.from,
          to: to,
          sign: md5(this.appKey + text + this.salt + this.key)
        },
        success: function (data) {
          vm.$set(vm.$data, 'translatedText', data.translation[0])
        }
      })
    }
  }
}
</script>

<style>
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }
</style>
