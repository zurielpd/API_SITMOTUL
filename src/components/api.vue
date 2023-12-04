<script setup>
import apicarreras from './apicarreras.vue';
import { computed, onMounted, ref } from 'vue';
import dayjs from 'dayjs'
const info = ref('')
const isLoading = ref('')

const infocarrera = ref('')
const isLoading2 = ref('')
//en el fronten
async function fetchData() {
    try {
        const response = await fetch('https://sitmotul.com.mx/api/statusEval');
        const data = await response.json();
        info.value = data
        isLoading.value = false
        console.log(info.value)
    } catch (error) {
        console.error('Error al obtener datos:', error);
    }
}

onMounted(() => {
    fetchData();
})

// const dayjs = require('dayjs')
const finicio = computed(() => {
    return dayjs(info.value.inicio).format('DD/MM/YYYY')
})



const ffin = computed(() => {
    return dayjs(info.value.fin).format('DD/MM/YYYY')
})

const tiempoRestante = computed(() => {
    const now = dayjs();
    const fin = dayjs(info.value.fin);


    const tiempoRestante = fin.diff(now, 'hour');
    return tiempoRestante;
})


const alFaltantes = computed(() => {
    const hecho = info.value.alEvaluados;
    const total = info.value.alTotal;

    const faltantes = total - hecho;

    return Math.round(faltantes);
})

const alumnosFaltantes = computed(() => {
    const hecho = info.value.alEvaluados;
    const total = info.value.alTotal;

    const faltantes = total - hecho;

    const faltan = (faltantes / total) * 100
    return Math.round(faltan);
})

const realizadas = computed(() => {
    const hecho = info.value.alEvaluados;
    const total = info.value.alTotal;

    const listo = (hecho / total) * 100
    return Math.round(listo);
})



//del backend




</script>


<template>
    <div class="flex flex-col justify-center items-center bg-[#ffdfab] w-full h-full">


        <h1 class="font-bold text-xl">SITMOTUL</h1>
        <h2 class="font-medium text-center mb-5">Estado de la evaluación tutor </h2>

        <div class=" mb-10 flex flex-col justify-center items-center space-y-10">

            <div class="w-96 h-32 bg-[#913f33] flex justify-center items-center rounded-full flex-col">
                <i class="fa-solid fa-calendar-days text-4xl text-white"></i>
                <p class="text-xl text-white font-bold">Periodo:</p>
                <p class="text-xl text-white font-bold">{{ info.periodo }}</p>
            </div>



            <div class="flex flex-col md:flex-row justify-center items-center md:space-x-10">

                <div class="flex flex-col md:space-x-5 justify-center items-center space-y-10">

                    <div class="w-96 h-32 bg-[#ffaa67] flex justify-center items-center rounded-full flex-row space-x-5">
                        <i class="fa-solid fa-calendar-days text-4xl text-white"></i>
                        <div class="flex flex-col justify-center items-center">
                            <p class="text-xl text-white font-bold">Fecha de inicio:</p>
                            <p class="text-xl text-white font-bold">{{ finicio }}</p>
                        </div>
                    </div>

                    <div class="w-96 h-32 bg-[#ffaa67] flex justify-center items-center rounded-full flex-row space-x-5">
                        <i class="fa-solid fa-calendar-days text-4xl text-white"></i>
                        <div class="flex flex-col justify-center items-center">
                            <p class="text-xl text-white font-bold">Fecha de finalización:</p>
                            <p class="text-xl text-white font-bold">{{ ffin }}</p>
                        </div>
                    </div>
                </div>

                <div
                    class="w-80 h-80 bg-[#ff705f] flex flex-col justify-center items-center rounded-3xl space-y-5 md:mt-0 mt-10">

                    <p class="text-3xl text-white font-bold">Tiempo restante:</p>
                    <div class="flex space-x-5">
                        <i class="fa-solid fa-clock text-4xl text-white"></i>
                        <p class="text-3xl text-white font-bold">{{ tiempoRestante }} horas</p>
                    </div>

                </div>
            </div>


        </div>

        <div class="flex flex-row space-x-5">


        </div>

        <div class="flex flex-col justify-center items-center space-y-5">

            <p class="text-xl text-black font-bold mb-5">Estado de las Evaluaciones</p>

            <div class="w-96 h-32 bg-[#913f33] flex justify-center items-center rounded-full flex-col">
                <i class="fa-solid fa-user text-4xl text-white"></i>
                <p class="text-xl text-white font-bold">Alumnos totales:</p>
                <p class="text-xl text-white font-bold">{{ info.alTotal }}</p>
            </div>

            <div
                class="md:w-[800px] md:h-[500px] w-[380px] h-[300px] bg-[#ff705f] flex flex-col justify-center items-center">


                <div
                    class="md:w-[600px] md:h-[350px] w-[350px] h-[250px] bg-[#ff705f] border-l-4 border-b-4 border-black space-y-12 ">

                    <i class="fa-solid fa-circle-check absolute -translate-x-14 translate-y-16 text-3xl text-black"></i>
                    <i class="fa-solid fa-circle-xmark absolute -translate-x-14 translate-y-44 text-3xl text-black"></i>
                    <div class="mt-12">
                        <div class=" md:h-20 h-10 bg-[#9fb9c2]" :style="{ 'width': realizadas + '%' }">

                        </div>

                        <p class="text-xl text-black font-bold">Evaluaciones realizadas: {{ info.alEvaluados }} o {{
                            realizadas }} %</p>
                    </div>

                    <div>
                        <div class=" md:h-20 h-10 bg-[#9fb9c2]" :style="{ 'width': alumnosFaltantes + '%' }">

                        </div>

                        <p class="text-xl text-black font-bold">Evaluaciones faltantes: {{ alFaltantes }} o {{
                            alumnosFaltantes }} %</p>
                    </div>


                </div>



            </div>
        </div>


        <apicarreras></apicarreras>
    </div>
</template>