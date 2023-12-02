<script setup>
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

// const dayjs = require('dayjs')
// //import dayjs from 'dayjs' // ES 2015
// dayjs().format()



</script>


<template>
    <!-- <table class="bg-white border border-gray-300">
    <thead>
        <tr class="bg-blue-200">
            <th class="py-2 px-4 border-b">Dato</th>
            <th class="py-2 px-4 border-b">Valor</th>
        </tr>
    </thead>

    <tbody>
        <tr>
            <td class="py-2 px-4 border-b">
                <ul>
                    <li>periodo</li>
                    <li>inicio</li>
                    <li>fin</li>
                    <li>altotal</li>
                    <li>alevaluados</li>
                </ul>
            </td>
           <td class="py-2 px-4 border-b bg-blue-600">
                <ul>
                    <li v-for="item in info " :key = "item" >{{ item }}</li>

                    {{ info.periodo }}
                </ul>
           </td>
            
         
        </tr>
      
    </tbody>
</table> -->

    <div class="flex flex-col justify-center items-center bg-[#ece1c3]">

        <img src="/sitmotul/assets/logoSitmotul-58d3b94c.svg" alt="logotipo del sitmotul" class="w-20 mx-auto mt-7">
        <h1 class="font-bold text-xl">SITMOTUL</h1>
        <h2 class="font-medium text-center mb-5">Estado de la evaluación tutor </h2>

        <div class=" mb-10 flex flex-col justify-center items-center space-y-10">

            <div class="w-96 h-32 bg-[#063940] flex justify-center items-center rounded-full flex-col">
                <i class="fa-solid fa-calendar-days text-4xl text-white"></i>
                <p class="text-xl text-white font-bold">Periodo:</p>
                <p class="text-xl text-white font-bold">{{ info.periodo }}</p>
            </div>



            <div class="flex flex-row justify-center items-center space-x-10">

                <div class="flex flex-col space-x-5 justify-center items-center space-y-10">

                    <div class="w-96 h-32 bg-[#3e838c] flex justify-center items-center rounded-full flex-row space-x-5">
                        <i class="fa-solid fa-calendar-days text-4xl text-white"></i>
                        <div class="flex flex-col justify-center items-center">
                            <p class="text-xl text-white font-bold">Fecha de inicio:</p>
                            <p class="text-xl text-white font-bold">{{ finicio }}</p>
                        </div>
                    </div>

                    <div class="w-96 h-32 bg-[#3e838c] flex justify-center items-center rounded-full flex-row space-x-5">
                        <i class="fa-solid fa-calendar-days text-4xl text-white"></i>
                        <div class="flex flex-col justify-center items-center">
                            <p class="text-xl text-white font-bold">Fecha de finalización:</p>
                            <p class="text-xl text-white font-bold">{{ ffin }}</p>
                        </div>
                    </div>
                </div>

                <div class="w-80 h-80 bg-[#195e63] flex flex-col justify-center items-center rounded-3xl space-y-5">

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

            <div class="w-96 h-32 bg-[#063940] flex justify-center items-center rounded-full flex-col">
                <i class="fa-solid fa-user text-4xl text-white"></i>
                <p class="text-xl text-white font-bold">Alumnos totales:</p>
                <p class="text-xl text-white font-bold">{{ info.alTotal }}</p>
            </div>

            <div class="w-[800px] h-[500px] bg-[#8ebdb6] flex flex-col justify-center items-center">


                <div class="w-[600px] h-[350px] bg-[#8ebdb6] border-l-4 border-b-4 border-black space-y-12">

                    <i class="fa-solid fa-circle-check absolute -translate-x-14 translate-y-16 text-3xl text-black"></i>
                    <i class="fa-solid fa-circle-xmark absolute -translate-x-14 translate-y-44 text-3xl text-black"></i>
                    <div class="mt-12">
                        <div class=" h-20 bg-[#195e63]" :style="{ 'widt': realizadas + '%' }">

                        </div>

                        <p class="text-xl text-black font-bold">Evaluaciones realizadas: {{ info.alEvaluados }} o {{
                            realizadas }} %</p>
                    </div>

                    <div>
                        <div class=" h-20 bg-[#3e838c]" :style="{ 'width': alumnosFaltantes + '%' }">

                        </div>

                        <p class="text-xl text-black font-bold">Evaluaciones faltantes: {{ alFaltantes }} o {{
                            alumnosFaltantes }} %</p>
                    </div>


                </div>

                <!-- <div class="flex flex-row space-x-9 pl-12">
                    <p class="text-xl text-white font-bold">100</p>
                    <p class="text-xl text-white font-bold">200</p>
                    <p class="text-xl text-white font-bold">300</p>
                    <p class="text-xl text-white font-bold">400</p>
                    <p class="text-xl text-white font-bold">500</p>
                    <p class="text-xl text-white font-bold">600</p>
                    <p class="text-xl text-white font-bold">700</p>
                    <p class="text-xl text-white font-bold">800</p>
                    <p class="text-xl text-white font-bold">900</p>
                </div> -->


            </div>
        </div>

        <p class="text-xl text-black font-bold mb-5 mt-5">Evaluaciones por carreras</p>

    </div>
</template>