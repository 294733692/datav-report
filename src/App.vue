<template>
  <div id="app">
    <div>
      <p>
        If Element is successfully added to this project, you'll see an
        <code v-text="'<el-button>'"></code>
        below
      </p>
      <el-button type="success">成功按钮</el-button>
    </div>
  </div>
</template>

<script>

export default {
  name: 'app'
}
</script>

<style>
html, body ,#app {
  width: 100%;
  height: 100%;
  padding: 0;
  margin: 0;
}
</style>
