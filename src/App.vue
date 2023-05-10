<template>
  <div id="app">
    <ve-line :data="data"></ve-line>
    <router-view/>
  </div>
</template>

<script>

export default {
  name: 'app',
  data () {
    return {
      data: {
        columns: ['日期', '销售额'],
        rows: [
          { 日期: '1月1日', 销售额: 123 },
          { 日期: '1月2日', 销售额: 1234 },
          { 日期: '1月3日', 销售额: 1243 },
          { 日期: '1月4日', 销售额: 12413 },
          { 日期: '1月5日', 销售额: 1223 }
        ]
      }
    }
  }
}
</script>

<style>
html, body, #app {
  width: 100%;
  height: 100%;
  padding: 0;
  margin: 0;
}
</style>
