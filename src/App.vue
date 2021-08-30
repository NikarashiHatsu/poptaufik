<template>
  <div style="backgroundColor: #ff2323" class="w-full h-screen flex items-center justify-center relative overflow-hidden">
    <div @click="touchs" class="w-full h-full absolute top-0 left-0 z-10"></div>

    <h1 class="text-4xl md:text-6xl absolute top-0 text-white font-bold mt-8 tracking-wide">POPTOPIK</h1>
    <h1 class="text-4xl md:text-6xl absolute top-0 text-white font-bold mt-20 md:mt-24 tracking-wide">{{ pops }}</h1>
    <img src="./assets/images/banteng_loli_pdip.jpg" class="w-full sm:w-auto sm:h-full top-0 bottom-0" />
    <img :src="tempik" class="absolute bottom-0 w-full sm:w-auto" />
  </div>
</template>

<script>
  import tempik1 from './assets/images/tempik1.png'
  import tempik2 from './assets/images/tempik2.png'
  import uhh from './assets/sounds/uhh.mp3'
  import kaget from './assets/sounds/kaget.mp3'

  export default {
    name: 'App',
    beforeMount() {
      this.pops = localStorage.getItem('pops') ?? 0
    },
    data() {
      return {
        pops: 0,
        clicked: false,
        soundUhh: new Audio(uhh),
        soundKaget: new Audio(kaget),
      }
    },
    methods: {
      touchs() {
        this.pops++
        this.clicked = true
        
        this.soundUhh.pause()
        this.soundKaget.pause()
        this.soundUhh.currentTime = this.soundKaget.currentTime = 0
        this.soundUhh.play()

        localStorage.setItem('pops', this.pops)

        setTimeout(() => {
          this.touche()
        }, 300);
      },
      touche() {
        this.clicked = false
        this.soundKaget.play()
      }
    },
    computed: {
      tempik() {
        return this.clicked 
          ? tempik2
          : tempik1
      }
    }
  }
</script>

<style scoped>
  h1 {
    -webkit-text-stroke-color: #000;
    -webkit-text-stroke-width: 1px;
  }
</style>