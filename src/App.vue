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
              <select class="form-select" v-model="catFilter">
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
              <select class="form-select" v-model="catColor">
                <option value="">Selecciona una opción</option>
                <option v-for="(color, index) in colores" :key="index" :value="color" v-text="color"></option>
              </select>
            </div>
            <div class="col-auto">
              <div class="colorize" :style="{backgroundColor: catColor}"></div>
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
          <img :src="catImg">
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
      catImg: '',
      catTitulo:"",
      catTamanio:"",
      titulo: "Random Gif Cat",
      catFilter: "",
      catColor: "",
      filtros: ['blur','mono','sepia','negative','paint','pixel'],
      colores:['Red', 'Blue', 'Green', 'Yellow', 'Purple']

    };
  },
  components: {
    HelloWorld,
  },

  methods: {
    obtenerGatito(){
     fetch(`https://cataas.com/cat/gif//says/${this.catTitulo}?size=${this.catTamanio}&color=${this.catColor}&filter=${this.catFilter}`)
      .then((res) => res.blob())
      .then((blob) => {
        let catUrl = URL.createObjectURL(blob)
        this.catImg = catUrl
      }) 
    },
    
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
