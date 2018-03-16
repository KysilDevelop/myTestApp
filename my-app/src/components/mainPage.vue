<template>
  <div>
    <header class="header header--pull-right">
      <a class="logo logo--pull-left" href="index.html">
        <img class="" src="../assets/logo.png" alt="Pluggedin">
      </a>
      <div class="nav">
        <a class="nav__text" href="#">Über uns</a>
        <a class="nav__text" href="#">Redaktion</a>
        <div class="nav__switcher">
          <span class="nav__chose">DE</span>
          <span class="nav__chose nav__chose--active">EN</span>
        </div>
      </div>

      <nav class="main-nav" aria-label="site">
        <ul class="main-nav__list">
          <li class="main-nav__item"><a class="main-nav__icon main-nav__icon--search" href="#" title="Home"></a></li>
          <li class="main-nav__item main-nav__item--left-border"><a href="#" title="Home">Design + lifestyle</a></li>
          <li class="main-nav__item main-nav__item--left-border"><a href="#" title="Home">Trends</a></li>
          <li class="main-nav__item main-nav__item--left-border"><a href="#" title="Home">Infodelight</a></li>
          <li class="main-nav__item main-nav__item--left-border"><a href="#" title="Home">Smart living</a></li>
        </ul>
      </nav>
    </header>
    <div class="slider slider--w75">
      <div class="slider__nav">
        <span class="slider__link slider__link--l-border">Design + lifestyle</span>
        <span class="slider__link slider__link--l-border slider__link--r-border">Smart living</span>
      </div>
      <h2 class="slider__title">Was hilft mir, Energie zu sparen und<br /> Spaß zu haben, bei mir zu Hause?</h2>
      <p class="slider__text">Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do<br /> eiusmod tempor incididunt ut  dolor in reprehenderit in quia...</p>
    </div>
    <aside class="aside aside--w25">
      <h2 class="aside__title">A place called Inspiration.</h2>
      <p class="aside__text">
        Neque porro quisquam est, qui dolorem ipsum quia dolor sit amet, consectetur, adipisci velit, sed quia non
        numquam eius modi tempora incidunt ut labore et dolore magnam voluptatem.
      </p>
      <label for="typeChart">Type</label>
      <select class="aside__select" name="typeChart" id="typeChart" v-model="selectChart">
        <option v-for="item in chartType" :value="item.type">{{item.name}}</option>
      </select>
      <!--<button class="aside__btn">Über die Autoren</button>-->
      <button @click="load" class="aside__btn">Insert</button>
    </aside>
    <div>
      <article class="article article--w50">
        <img src="../assets/slide-2.jpg" alt="Pluggedin design" sizes>
        <h2 class="article__title">Was hilft mir, Energie zu sparen und Spaß zu haben, bei mir zu Hause?</h2>
        <p class="article__text">Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut  dolor in reprehenderit in quia...</p>
      </article>

      <article class="article article--w50">
        <img src="../assets/slide-3.jpg" alt="Pluggedin design" sizes="100w">
        <h2 class="article__title">Was hilft mir, Energie zu sparen und Spaß zu haben, bei mir zu Hause?</h2>
        <p class="article__text">Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut  dolor in reprehenderit in quia...</p>
      </article>
    </div>
    <div id="charts">
      <vue-highcharts :options="options" ref="lineCharts"></vue-highcharts>
    </div>
    <div id="message-event-example" class="demo">
      <p v-for="msg in messages">{{ msg }}</p>
      <button-message v-on:message="handleMessage"></button-message>
    </div>
  </div>

</template>


<script>
  import VueHighcharts from 'vue2-highcharts'
  const asyncData = {
    name: 'Tokyo',
    marker: {
      symbol: 'square'
    },
    data: [7.0, 6.9, 9.5, 14.5, 18.2, 21.5, 25.2, {
      y: 26.5,
      marker: {
        symbol: 'url(http://www.highcharts.com/demo/gfx/sun.png)'
      }
    }, 23.3, 18.3, 13.9, 9.6]
  }
  export default{
    name: 'page',
    components: {
      VueHighcharts
    },
    data(){
      return{
        selectChart: '',
        chartType: [
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
        options: {
          chart: {
            type: this.selectChart
          },
          title: {
            text: 'Monthly Average Temperature'
          },
          subtitle: {
            text: 'Source: WorldClimate.com'
          },
          xAxis: {
            categories: ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun',
              'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec']
          },
          yAxis: {
            title: {
              text: 'Temperature'
            },
            labels: {
              formatter: function () {
                return this.value + '°';
              }
            }
          },
          tooltip: {
            crosshairs: true,
            shared: true
          },
          credits: {
            enabled: false
          },
          plotOptions: {
            spline: {
              marker: {
                radius: 4,
                lineColor: '#666666',
                lineWidth: 1
              }
            }
          },
          series: []
        }
      }
    },
    methods: {
      load(){
        let lineCharts = this.$refs.lineCharts;
        lineCharts.delegateMethod('showLoading', 'Loading...');
        setTimeout(() => {
          lineCharts.$options.propsData.options.chart.type = this.selectChart;
          lineCharts.addSeries(asyncData);
          lineCharts.hideLoading();
        }, 2000)
      }
    }
  }
  Vue.component('button-message', {
    template: `<div>
    <input type="text" v-model="message" />
    <button v-on:click="handleSendMessage">Отправить</button>
  </div>`,
    data: function () {
      return {
        message: 'тестовое сообщение'
      }
    },
    methods: {
      handleSendMessage: function () {
        this.$emit('message', { message: this.message })
      }
    }
  })

  new Vue({
    el: '#message-event-example',
    data: {
      messages: []
    },
    methods: {
      handleMessage: function (payload) {
        this.messages.push(payload.message)
      }
    }
  })
</script>
