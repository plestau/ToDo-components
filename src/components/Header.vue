<script setup>
 import {ref} from 'vue';

defineProps({
    recordatorios: {
        type: Array,
        required: true,
    },
});

let texto = ref("");

function nuevaNota(array){
    if (texto.value != "") {
        let nuevaNota = {
            id: array.length + 1,
            titulo: texto.value,
            hecho: false,
            prioridad: 2,
            fecha: Date.now()
        };
        array.push(nuevaNota);
        texto.value = "";
    }
    localStorage.setItem("recordatorios", JSON.stringify(array));
}
</script>

<template>
    <header>
      <h1>Reminder</h1>
      <input
        type="text"
        id="reminder"
        placeholder="¿Qué quieres recordar?"
        v-model="texto"
        @keyup.enter="nuevaNota(recordatorios)"
      />
    </header>
</template>