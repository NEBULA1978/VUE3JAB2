<template>
    <div>
        <h2>Cena {{ contador + 1 }} con el rey godo {{ rey }}</h2>
        <h3 class="precio">Precio: {{ productos[contador].precio }}€</h3>
        <div class="todosLosDias dias" v-if="productos[contador].finDeSemana">(Solo fines de semana)</div>
        <div class="dias soloFinesDeSemana" v-else>(De Lunes a Domingo)</div>
        <div v-if="productos[contador].precio < 100" class="oferta">
            <div>Ahorra un 10% dto: {{ nuevoPrecio }}€</div>
            <img src="/oferta.jpg" alt="rey godo en descuento" />
        </div>
        <img :src="imagen" alt="">
        <button @click="siguiente">Siguiente ({{ contador + 1 }} / {{ total }})</button>
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
/* Estilos aquí */
</style>
