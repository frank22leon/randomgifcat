<template>
  <div id="app">
    <div class="container-fluid header">
      <h1>Random GIF Cat</h1>
    </div>

    <form @submit.prevent="handleOnSubmit">
      <div class="container-fluid hero-section">
        <div>
          <label class="pr-1">Titulo: </label>
          <input
            type="text"
            v-model="form.titulo"
            required
            placeholder="Escriba un titulo"
          />
        </div>

        <div>
          <label class="pr-1">Filtro: </label>
          <select v-model="form.filtro" required>
            <option disabled selected value="">Elige un filtro</option>
            <option value="blur">Blur</option>
            <option value="mono">Mono</option>
            <option value="sepia">Sepia</option>
            <option value="negative">Negative</option>
            <!-- Pixel no funciona -->
            <option value="pixel">Pixel</option>
          </select>
        </div>

        <div
          class="circle-color"
          :style="{ 'background-color': form.color }"
        ></div>

        <div>
          <label class="select-color pr-1">Color: </label>
          <select v-model="form.color">
            <option value="" disabled selected>Elige un color</option>
            <option value="green">Verde</option>
            <option value="blue">Azul</option>
            <option value="red">Rojo</option>
            <option value="yellow">Amarillo</option>
            <option value="orange">Naranjo</option>
          </select>
        </div>

        <div>
          <label class="pr-1">Tamaño: </label>
          <input
            type="number"
            min="30"
            v-model.number="form.tamaño"
            required
            placeholder="Ingrese un tamaño"
          />
        </div>
      </div>
      <div class="container-fluid img-section">
        <button type="submit">
          {{ 'Obtener mi gatito' }}
        </button>
      </div>
    </form>
    <img :src="urlCat" class="cat" />
  </div>
</template>

<script>
export default {
  name: 'App',
  data: () => ({
    form: {
      titulo: '',
      filtro: '',
      color: '',
      tamaño: ''
    },
    urlCat: ''
  }),
  methods: {
    async handleOnSubmit() {
      this.urlCat = `https://cataas.com/cat/gif/says/${this.form.titulo}?${this.formConfig}`
    }
  },
  computed: {
    formConfig() {
      return `filter=${this.form.filtro}&color=${this.form.color}&size=${this.form.tamaño}`
    }
  }
}
</script>

<style lang="scss">
html {
  background-color: lightblue;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.header {
  background-color: lightblue;
  padding: 40px;
}
.hero-section {
  background-color: lightcoral;
  padding: 40px;
  margin: 0;
}

.select-color {
  float: center;
}

.img-section {
  background-color: lightblue;
  padding: 40px;
}
.cat {
  width: 100%;
  display: inline-flex;
  padding: 0 35% 5% 35%;
  box-sizing: border-box;
  background-color: lightblue;
}

.circle-color {
  height: 30px;
  border-radius: 15px;
  width: 30px;
  border: 1px solid lightgray;
  margin: 0 10px;
  align-items: right;
  float: right;
}
</style>
