<template>
  <div id="App">
    <div class="container">
      <p class="d-flex justify-content-center" :class="['h1', 'text-center', 'mt-5']">{{ titulo }}<img class="ms-2" src="https://img.icons8.com/ios/50/000000/cat-profile.png"/> </p>
    </div>

    <div class="container">
      <div class="d-flex justify-content-center">
        <form @submit.prevent="obtenerGatito">
          <div class="row g-3 align-items-center my-2">
            <div class="col-auto">
              <label class="col-form-label ancho"> Titulo </label>
            </div>
            <div class="col-auto">
              <input type="text" class="form-control" v-model="catTitulo" />
            </div>
            <div class="col-auto">
              <span class="form-text">
                Ingrese el titulo para la imagen .
              </span>
            </div>
          </div>

          <div class="row g-3 align-items-center my-2">
            <div class="col-auto">
              <label class="col-form-label ancho"> Filtro </label>
            </div>
            <div class="col-auto">
              <select class="form-select" @change="catFilter($event)">
                <option value="">Selecciona una opción</option>
                <option v-for="(filtro, index) in filtros" :key="index" :value="filtro" v-text="filtro"></option>
              </select>
            </div>
            <div class="col-auto">
              <span class="form-text">
                Seleccione el filtro para la imagen .
              </span>
            </div>
          </div>

          <div class="row g-3 align-items-center my-2">
            <div class="col-auto">
              <label class="col-form-label ancho"> Color </label>
            </div>
            <div class="col-auto">
              <select class="form-select" @change="catColor($event)">
                <option value="">Selecciona una opción</option>
                <option v-for="(c, index) in colores" :key="index" :value="c.color" v-text="c.texto"></option>
              </select>
            </div>
            <div class="col-auto">
              <div class="colorize" :style="{backgroundColor: color}"></div>
            </div>
            <div class="col-auto">
              <span class="form-text">
                Seleccione el color del texto
              </span>
            </div>
          </div>

          <div class="row g-3 align-items-center my-2">
            <div class="col-auto">
              <label class="col-form-label ancho"> Tamaño </label>
            </div>
            <div class="col-auto">
              <input type="text" class="form-control" v-model="catTamanio" />
            </div>
            <div class="col-auto">
              <span class="form-text">
                Ingrese el tamaño en numeros enteros Ej : <strong>450</strong>
              </span>
            </div>
            <button type="submit" class="btn btn-outline-dark">- Obtener Gatito -</button>
          </div>
        </form>
      </div>
    </div>
    <div class="container mt-5">
      <h2 class="text-center">Este es tu gato 🙀</h2>
      <div class="d-flex justify-content-center mb-2">
        <div class="catContainer">
          <img :src="imagen">
      </div>
      </div>
    </div>
  </div>
  <HelloWorld msg="Welcome to Your Vue.js App" />
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";

export default {
  name: "App",
  data() {
    return {
      imagen: '',
      catTitulo:"",
      catTamanio:"",
      titulo: "Random Gif Cat",
      filtro: "",
      color: "",
      filtros: ['blur','mono','sepia','negative','paint','pixel'],
      colores:[
        {color: 'green', texto: 'Verde'},
        {color: 'blue', texto: 'Azul'},
        {color: 'red', texto: 'Rojo'},
        {color: 'white', texto: 'Blanco'},
        {color: 'black', texto: 'Negro'},
        ]

    };
  },
  components: {
    HelloWorld,
  },

  methods: {
    obtenerGatito(){
      this.imagen = this.urlGatito
    },
    catFilter(event){
      this.filtro = event.target.value
    },
    catColor(event){
      this.color = event.target.value
    }
  },
  computed: {
    urlGatito(){
      return `https://cataas.com/cat/gif/says/${this.catTitulo}?filter=${this.filtro}&color=${this.color}&size=${this.catTamanio}`
    }
  },
};
</script>

<style>
.ancho{
  width: 75px;
}
input{
  width: 250px !important;
}
select{
  width: 250px !important;
}
.colorize{
  width: 20px;
  height: 20px;
  background-color: red;
  border-radius: 15px;
}
.catContainer{
  width: 800px;
  height: 400px;
  border: 1px solid black;
  border-radius: 5px;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
