<template>
  <div class="cabecera">
    <h1>Clicka en estas galletitas</h1>
    <p>Puntuacion: {{ puntuacion }}</p>
    <p>Ganacia pasiva: {{ puntuacionPasiva }}</p>


  </div>
  <center>
    <button class="galleta" @click="puntuarConClick"></button>
    <p></p>
    <div class="botones">
      <button :disabled="!checkBoton1" @click="primeraCompra">Primera mejora: {{ boton1Precio }}$</button>
      <button :disabled="!checkBoton2" @click="segundaCompra">Segunda mejora: {{ boton2Precio }}$</button>
      <button :disabled="!checkBoton3" @click="terceraCompra">Tercera mejora: {{ boton3Precio }}$</button>
    </div>
  </center>
</template>

<script>

export default {
  data() {
    return {
      puntuacion: 0,
      puntuacionPasiva: 0,
      boton1Precio: 10,
      boton2Precio: 25,
      boton3Precio: 50,
      checkBoton1: false,
      checkBoton2: false,
      checkBoton3: false
    }
  },
  methods: {
    primeraCompra() {
      this.puntuacion -= 10
      this.puntuacionPasiva++
      this.boton1Precio = parseInt(this.boton1Precio * 1.1)
    },
    segundaCompra() {
      this.puntuacion -= 25
      this.puntuacionPasiva = this.puntuacionPasiva + 5
      this.boton2Precio = parseInt(this.boton2Precio * 1.1)

    },
    terceraCompra() {
      this.puntuacion -= 50
      this.puntuacionPasiva = this.puntuacionPasiva + 10
      this.boton3Precio = parseInt(this.boton3Precio * 1.1)

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
  background-image: url('./assets/galletita.png');
  background-repeat: no-repeat;
  background-size: contain;
  height: 300px;
  width: 300px;
  border: none;
  cursor:pointer;
}

.cabecera {
  display: inline;
}

.botones {
  display: inline;
}
</style>
