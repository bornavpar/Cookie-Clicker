<template>
  <div class="cabecera">
    <h1>Clicka en estas galletitas</h1>
    <p>Puntuacion: {{ puntuacion }}</p>
    <p>Ganacia pasiva: {{ puntuacionPasiva }}</p>


  </div>
  <center>
    <button class="galleta" @click="puntuarConClick">Galletita</button>
    <p></p>
    <div class="botones">
      <button :disabled="!checkBoton1" @click="primeraCompra">Primera mejora</button>
      <button :disabled="!checkBoton2" @click="segundaCompra">Segunda mejora</button>
      <button :disabled="!checkBoton3" @click="terceraCompra">Tercera mejora</button>
    </div>
  </center>
</template>

<script>

export default {
  data() {
    return {
      puntuacion: 0,
      puntuacionPasiva: 0,
      checkBoton1: false,
      checkBoton2: false,
      checkBoton3: false
    }
  },
  methods: {
    primeraCompra() {
      this.puntuacion -= 10
      this.puntuacionPasiva++
    },
    segundaCompra() {
      this.puntuacion -= 25
      this.puntuacionPasiva = this.puntuacionPasiva + 5
    },
    terceraCompra() {
      this.puntuacion -= 50
      this.puntuacionPasiva = this.puntuacionPasiva + 10
    },
    puntuarConClick() {
      this.puntuacion++
    }
  },
  watch: {
    puntuacion(newValue) {
      if (newValue >= 10) {
        this.checkBoton1 = true;
      } else {
        this.checkBoton1 = false;
      }
      if (newValue >= 25) {
        this.checkBoton2 = true;
      } else {
        this.checkBoton2 = false;
      }
      if (newValue >= 50) {
        this.checkBoton3 = true;
      } else {
        this.checkBoton3 = false;
      }
    }
  },
  mounted() {
    setInterval(() => {
      if (this.puntuacionPasiva > 0) {
        this.puntuacion += this.puntuacionPasiva
      }
    }, 1000)
  }
};
</script>

<style>
.galleta {
  height: 100px;
  width: 100px;
  border-radius: 50%;
}

.cabecera {
  display: inline;
}

.botones {

  display: inline;
}
</style>
