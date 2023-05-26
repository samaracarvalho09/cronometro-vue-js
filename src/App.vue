<template>
  <div>
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

</template>


<script>
import { PhPlayPause, PhArrowUUpLeft, PhPlayCircle } from '@phosphor-icons/vue'

export default {
  components: {
    PhPlayPause,
    PhArrowUUpLeft,
    PhPlayCircle
  },

  data() {
    return {
      time: 0,
      cronometro: null,
      cronometroAtivo: false
    };
  },

  computed: {
    tempoFormatado() {
      const horas = Math.floor(this.time / 3600);
      const minutos = Math.floor((this.time % 3600) / 60);
      const segundos = this.time % 60;
      // const milissegundos = this.time % 1000;
      return `${this.formatarNumero(horas)}:${this.formatarNumero(minutos)}:${this.formatarNumero(segundos)}`;

    }
  },

  methods: {
    play() {
      this.cronometroAtivo = true
      this.cronometro = setInterval(() => {
        this.time++
      }, 1000);
      console.log('play')
    },

    pause() {
      this.cronometroAtivo = false;
      clearInterval(this.cronometro)
      this.cronometro = null;
      console.log('pause')
    },

    reset() {
      this.time = 0
      this.pause()
    },

   formatarNumero(valor) {
    return valor.toString().padStart(2, '0')
   }
}
}
</script>







<style scoped>
* {
  margin: 0px;
  padding: 0px;
  box-sizing: border-box;
}

.container {
  width: 100vw;
  //height: 100vh;
  background: linear-gradient(180deg, #e4b0c2 0%, #a8003b 100%);

  display: flex;
  flex-direction: column;
  align-items: center;
  padding-top: 120px;

  font-family: 'Roboto', sans-serif;
  color: #fbfbfb;
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
