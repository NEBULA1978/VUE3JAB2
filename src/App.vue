<template>
  <h2>Cena {{ contador + 1 }}
    con el rey godo {{ rey }}
  </h2>
  <button @:click="siguiente">Siguiente ({{ contador + 1 }}/ {{ total }} )</button>
</template>

<script setup>
import { ref, computed } from "vue"
import { productos } from "./datos.js"
const contador=ref(0)
const total = productos.length;
const siguiente = () => {
  // Increment the value of contador
  contador.value++
  // Check if contador is greater than or equal to total
  if (contador.value >= total) {
    // If so, reset contador back to 0
    contador.value = 0;
  }
}
const rey=computed(()=>{
  const elNombre = productos[contador.value].nombre.toLowerCase()
  
  return elNombre.substring(0, 1).toUpperCase() + elNombre.substring(1)
  
})
</script>

<style scoped></style>
