<template>
  <!-- <div id="minhaDiv" :style="`background-image: ${corDeFundo}`">-->
    <div id="minhaDiv" :style="{ 'background-image': corDeFundo }"> 
    <div class="wrapper-page">


      <button v-if="showDarkTheme" @click="alterarBackground('dark')" class="changeTheme">        
        <ph-moon :size="32" />
      </button>      
      <button v-else @click="alterarBackground('light')" class="changeTheme">

      <ph-sun :size="32" />
      </button>


      <div class="container">
        <div><span>Click to start!</span></div>
        <div class="valor-contador">{{ tempoFormatado }}</div>
        <div class="contador-icons">
          <button @click="reset">
            <ph-arrow-u-up-left :size="51" />
          </button>
          <button @click="play" :disabled="cronometroAtivo">
            <ph-play-circle :size="94" />
          </button>
          <button @click="pause" :disabled="!cronometroAtivo">
            <ph-play-pause :size="51" />
          </button>
        </div>
      </div>
    </div>
  </div>
</template>


<script>
import { PhPlayPause, PhArrowUUpLeft, PhPlayCircle, PhMoon, PhSun } from '@phosphor-icons/vue'
export default {
  components: {
    PhPlayPause,
    PhArrowUUpLeft,
    PhPlayCircle,
    PhMoon,
    PhSun,
    
  },

  data() {
    return {
      time: 0,
      cronometro: null,
      cronometroAtivo: false,
      corDeFundo: 'linear-gradient(180deg, #e4b0c2 0%, #a8003b 100%)',
      showDarkTheme: false,
      tema: 'light',


    }
  },
  created() {
    this.alterarBackground(this.tema);
  }, 

  computed: {
    tempoFormatado() {
      const horas = Math.floor(this.time / 3600)
      const minutos = Math.floor((this.time % 3600) / 60)
      const segundos = this.time % 60
      return `${this.formatarNumero(horas)}:${this.formatarNumero(minutos)}:${this.formatarNumero(
        segundos
      )}`
    }
  },

  methods: {
    play() {
      this.cronometroAtivo = true
      this.cronometro = setInterval(() => {
        this.time++
      }, 1000)
      console.log('play')
    },

    pause() {
      this.cronometroAtivo = false
      clearInterval(this.cronometro)
      this.cronometro = null
      console.log('pause')
    },

    reset() {
      this.time = 0
      this.pause()
    },

    formatarNumero(valor) {
      return valor.toString().padStart(2, '0')
    },
  //   alterarBackground() {
  //   this.corDeFundo = 'linear-gradient(180deg, #2D2B2C 0%, #090406 100%)';
  // }

 
  alterarBackground(tema) {

    if (tema === 'light') {
      this.corDeFundo = 'linear-gradient(180deg, #e4b0c2 0%, #a8003b 100%)'
    } else if (tema === 'dark') {
      this.corDeFundo = 'linear-gradient(180deg, #2D2B2C 0%, #090406 100%)'
    }
    
    this.showDarkTheme = !this.showDarkTheme;
  }
}
}
</script>

<style scoped>
* {
  margin: 0px;
  padding: 0px;
  box-sizing: border-box;
  max-width: 100vw;
  max-height: 100vh;
}

.wrapper-page {
  width: 100vw;
  
  display: flex;
  flex-direction: column;

  font-family: 'Roboto', sans-serif;
  color: #fbfbfb;
  overflow-x: hidden;
  overflow-y: hidden;
}

.changeTheme {
  padding: 30px;
  display: flex;
  justify-content: flex-end;
}

.changeDarkTheme {
  background: yellow;
}

.changeTheme svg {
  cursor: pointer;
}

.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding-top: 120px;
}

.container div span {
  font-size: 3.25rem;
  padding-bottom: 50px;
}

.valor-contador {
  padding-block: 100px;
  font-size: 3rem;
}
button {
  background: transparent;
  border: none;
  color: white;
  cursor: pointer;
}
.contador-icons {
  display: flex;
  align-items: center;
  gap: 50px;

  padding-bottom: 100px;
}
</style>
