<template>
  <div class="home">
    <top-view />
    <sales-view />
    <bottom-view />
    <map-view />
  </div>
</template>

<script>
import topView from '../components/TopView'
import salesView from '../components/SalesView'
import bottomView from '@/components/BottomView'
import mapView from '@/components/MapView'

export default {
  name: 'Home',
  components: {
    topView,
    salesView,
    bottomView,
    mapView
  }
}
</script>

<style lang="scss">
.home {
  height: 100%;
  widht: 100%;
  background: #eee;
  padding: 20px;
  box-sizing: border-box;
}
</style>
