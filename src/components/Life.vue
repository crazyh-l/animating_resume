
<template>
   <transition enter-active-class="animated zoomInLeft" leave-active-class="animated zoomOutRight">
  <div class="life">
      <header class="cd-header">
      <div id="cd-logo"><a href="https://cn.vuejs.org/">
          <img src="../assets/logo.png" v-bind:style="{ width: logoWidth + 'px', height: logoHeight + 'px' }">
        </a>
      </div>

    <nav class="cd-main-nav">
      <ul>
        <!-- inser more links here -->
        <li><a href="#0">诗</a></li>
        <li><a href="#0">远方</a></li>
        <li><a href="#0">劈柴</a></li>
        <li><a href="#0">喂马</a></li>
      </ul>
    </nav> <!-- cd-main-nav -->
  </header>

  <main class="cd-main-content" id="app">
      <poetryTitle/>
      <poetry/>
      <distanceTitle/>
      <distance/>
      <chopWoodTitle/>
      <chopWood/>
      <horses/>
  </main>
  </div>
  </transition>
</template>

<script>
import '../assets/style.css'
import 'vue2-animate/dist/vue2-animate.min.css';
import poetryTitle    from '../components/PoetryTitle'
import poetry         from '../components/Poetry'
import distanceTitle  from '../components/DistanceTitle'
import distance       from '../components/Distance'
import chopWoodTitle  from '../components/ChopWoodTitle'
import chopWood       from '../components/ChopWood'
import horses         from '../components/horses'

export default {
  name: 'life',
  data(){
    return {
        logoWidth: 30,
        logoHeight:30
    }
  },
  components: {
    poetryTitle,
    poetry,
    distanceTitle,
    distance,
    chopWoodTitle,
    chopWood,
    horses
  }
}

</script>

<style>
.life{ width:48vw;height: 100%; display: none;  position: absolute;right:0;top:0;}
@media screen and (max-width: 600px) {
  .cd-header {
    display: none
  }
  .life{ width:92vw;height: 100%; display: none;  position: absolute;left:0;bottom:0;}
}
</style> 
