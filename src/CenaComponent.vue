<template>
    <div class="cena-component">
        <h2>Cena {{ contador + 1 }} con el rey godo {{ rey }}</h2>
        <h3 class="precio">Precio: {{ productos[contador].precio }}€</h3>
        <div class="dias"
            :class="{ 'todosLosDias': productos[contador].finDeSemana, 'soloFinesDeSemana': !productos[contador].finDeSemana }">
            {{ productos[contador].finDeSemana ? 'Solo fines de semana' : 'De Lunes a Domingo' }}
        </div>
        <div v-if="productos[contador].precio < 100" class="oferta">
            <div>Ahorra un 10% dto: {{ nuevoPrecio }}€</div>
            <img src="/oferta.jpg" alt="rey godo en descuento" />
        </div>
        <div class="image-container">
            <img :src="imagen" alt="" class="product-image">
        </div>
        <div class="button-container">
            <button @click="siguiente">Siguiente ({{ contador + 1 }} / {{ total }})</button>
        </div>
    </div>
</template>

<script setup>
import { ref, computed } from "vue"
import { productos } from "./datos.js"

const contador = ref(0)
const total = productos.length
const ruta = "https://www.html6.es/img/rey_"

const siguiente = () => {
    contador.value++
    if (contador.value >= total) {
        contador.value = 0
    }
}

const rey = computed(() => {
    const elNombre = productos[contador.value].nombre.toLowerCase()
    return elNombre.substring(0, 1).toUpperCase() + elNombre.substring(1)
})

const imagen = computed(() => {
    return `${ruta}${productos[contador.value].nombre.toLowerCase()}.png`
})

const nuevoPrecio = computed(() => {
    return (productos[contador.value].precio / 1.10).toFixed(2)
})
</script>

<style scoped>
.cena-component {
    max-width: 600px;
    margin: 0 auto;
    padding: 20px;
    background-color: white;
    box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.1);
    text-align: center;
}

.dias {
    color: white;
    padding: 4px 17px;
    font-size: 0.9em;
    border-radius: 4px;
    margin: 5px 0 10px;
    display: inline-block;
}

.todosLosDias {
    background-color: green;
}

.soloFinesDeSemana {
    background-color: red;
}

.precio {
    margin-bottom: 15px;
}

.oferta img {
    width: 65px;
    margin: 12px 5px;
}

button {
    background-color: #007bff;
    color: white;
    border: none;
    padding: 10px 20px;
    border-radius: 4px;
    cursor: pointer;
}

.image-container {
  text-align: center;
  margin-bottom: 20px;
}

.product-image {
  width: 100%; /* Asegura que las imágenes tengan el mismo ancho */
  max-height: 300px; /* Ajusta la altura máxima de las imágenes */
  object-fit: contain; /* Mantiene la proporción de la imagen y la ajusta dentro del contenedor */
}

.image-container {
  text-align: center;
  margin-bottom: 20px;
}

.product-image {
  width: 100%; /* Asegura que las imágenes tengan el mismo ancho */
  max-height: 300px; /* Ajusta la altura máxima de las imágenes */
  object-fit: contain; /* Mantiene la proporción de la imagen y la ajusta dentro del contenedor */
}

.button-container {
  display: flex;
  justify-content: center;
  margin-top: 20px;
}
button {
  /* Estilos anteriores del botón ... */
  position: fixed; /* Fija el botón en la posición */
  bottom: 20px; /* Espacio desde abajo */
  right: 20px; /* Espacio desde la derecha */
  z-index: 1; /* Asegura que el botón esté por encima de otros elementos */
}
</style>
