<template>
  <div id="app">
    <header-app></header-app>
    <slider-app></slider-app>
    <aside-app :list="chartList"></aside-app>
    <article-app></article-app>
    <charts-app></charts-app>
  </div>
</template>

<script>
import HeaderApp from './components/HeaderApp'
import SliderApp from './components/SliderApp'
import AsideApp from './components/AsideApp'
import ArticleApp from './components/ArticleApp'
import ChartsApp from './components/ChartsApp'

export default {
  name: 'App',
  data(){
    return {
      chartList: [
        {
          name: 'Select type',
          type: ''
        },
        {
          name: 'Bar',
          type: 'bar'
        },
        {
          name: 'Pie',
          type: 'pie'
        },
        {
          name: 'Line',
          type: 'line'
        },
      ],
      selectedChart: '',
    }
  },
  components: {
    HeaderApp,
    SliderApp,
    AsideApp,
    ArticleApp,
    ChartsApp
  },
  created() {
    this.$root.$on('add', (selected) => {
      this.selectedChart = selected;
      console.log('2', selected);
    })
  }
}
</script>

<style lang="scss">
  @import 'styles/normalize.scss';
  @import 'styles/style.scss';
</style>
