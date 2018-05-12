<template>
  <div>
    <!--加上页面修饰符，提交时就不回再重载页面-->
    <form v-on:submit.prevent="formSubmit">
      <input type="text" v-model="text" placeholder="输入需要翻译的内容"/>
      <select v-model="to">
        <option value ="en">英文</option>
        <option value ="ko">韩文</option>
        <option value ="fr">法文</option>
        <option value ="ru">俄文</option>
      </select>
      <input type="submit" value="翻译"/>
    </form>
  </div>
</template>

<script>
export default {
  name: 'TranslateForm',
  data: function () {
    return {
      text: '',
      to: 'en'
    }
  },
  methods: {
    formSubmit: function () {
      this.$emit('formSubmit', this.text, this.to)
    }
  }
}
</script>

<style></style>
