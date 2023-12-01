<script setup>
import { onMounted, ref } from 'vue';

const infocarrera = ref('')
const isLoading2 = ref('')
//en el fronten


async function fetchData2() {
    try {
        const response = await fetch('https://sitmotul.com.mx/api/statusEvalIng');
        const data = await response.json();
        infocarrera.value = data
        isLoading2.value = false
        console.log(infocarrera.value)
    } catch (error) {
        console.error('Error al obtener datos:', error);
    }
}

onMounted(() => {
    fetchData2();
})
//del backend



</script>


<template>
    <p>{{ infocarrera.ISC.listas }}</p>
</template>