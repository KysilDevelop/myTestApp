<template>
  <header class="header header--pull-right">
    <a class="logo logo--pull-left" href="#">
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
        <li class="main-nav__item">
          <a class="main-nav__link main-nav__link--search" href="#" title="Home"></a>
        </li>
        <li class="main-nav__item main-nav__item--left-border">
          <a class="main-nav__link" href="#" title="Home">Design + lifestyle</a>
        </li>
        <li class="main-nav__item main-nav__item--left-border">
          <a class="main-nav__link" href="#" title="Home">Trends</a>
        </li>
        <li class="main-nav__item main-nav__item--left-border">
          <a class="main-nav__link" href="#" title="Home">Infodelight</a>
        </li>
        <li class="main-nav__item main-nav__item--left-border">
          <a class="main-nav__link" href="#" title="Home">Smart living</a>
        </li>
      </ul>
    </nav>
  </header>
</template>

<script>
  export default {
    name: 'HeaderApp',
    data () {
      return {
        msg: 'Welcome to Header'
      }
    }
  }
</script>

