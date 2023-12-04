<script setup>
import { computed, onMounted, ref } from 'vue';

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

//modal ISC
const Modal = ref(false);

const openModal = () => {
    Modal.value = true;
};

const closeModal = () => {
    Modal.value = false;
};

// modal IEM
const ModalIEM = ref(false);

const openModalIEM = () => {
    ModalIEM.value = true;
};

const closeModalIEM = () => {
    ModalIEM.value = false;
};

// modal IER
const ModalIER = ref(false);

const openModalIER = () => {
    ModalIER.value = true;
};

const closeModalIER = () => {
    ModalIER.value = false;
};

// modal IE
const ModalIE = ref(false);

const openModalIE = () => {
    ModalIE.value = true;
};

const closeModalIE = () => {
    ModalIE.value = false;
};

// modal II
const ModalII = ref(false);

const openModalII = () => {
    ModalII.value = true;
};

const closeModalII = () => {
    ModalII.value = false;
};

//funciones ISC
const totalISC = ref(0);
const calcularTotalISC = computed(() => {
    totalISC.value = infocarrera.value.ISC.listas + infocarrera.value.ISC.faltantes;
    return (totalISC)
})

const realizadasISC = computed(() => {
    const hecho = infocarrera.value.ISC.listas;
    const total = totalISC.value;

    const listo = (hecho / total) * 100
    return Math.round(listo);
})

const evFaltantesISC = computed(() => {
    const faltantes = infocarrera.value.ISC.faltantes;
    const total = totalISC.value;

    const faltan = (faltantes / total) * 100
    return Math.round(faltan);
})


//funciones IEM
const totalIEM = ref(0);
const calcularTotalIEM = computed(() => {
    totalIEM.value = infocarrera.value.IEM.listas + infocarrera.value.IEM.faltantes;
    return (totalIEM)
})

const realizadasIEM = computed(() => {
    const hecho = infocarrera.value.IEM.listas;
    const total = totalIEM.value;

    const listo = (hecho / total) * 100
    return Math.round(listo);
})

const evFaltantesIEM = computed(() => {
    const faltantes = infocarrera.value.IEM.faltantes;
    const total = totalIEM.value;

    const faltan = (faltantes / total) * 100
    return Math.round(faltan);
})


//funciones IER
const totalIER = ref(0);
const calcularTotalIER = computed(() => {
    totalIER.value = infocarrera.value.IER.listas + infocarrera.value.IER.faltantes;
    return (totalIER)
})

const realizadasIER = computed(() => {
    const hecho = infocarrera.value.IER.listas;
    const total = totalIER.value;

    const listo = (hecho / total) * 100
    return Math.round(listo);
})

const evFaltantesIER = computed(() => {
    const faltantes = infocarrera.value.IER.faltantes;
    const total = totalIER.value;

    const faltan = (faltantes / total) * 100
    return Math.round(faltan);
})

//funciones IE
const totalIE = ref(0);
const calcularTotalIE = computed(() => {
    totalIE.value = infocarrera.value.IE.listas + infocarrera.value.IE.faltantes;
    return (totalIE)
})

const realizadasIE = computed(() => {
    const hecho = infocarrera.value.IE.listas;
    const total = totalIE.value;

    const listo = (hecho / total) * 100
    return Math.round(listo);
})

const evFaltantesIE = computed(() => {
    const faltantes = infocarrera.value.IE.faltantes;
    const total = totalIE.value;

    const faltan = (faltantes / total) * 100
    return Math.round(faltan);
})

//funciones II
const totalII = ref(0);
const calcularTotalII = computed(() => {
    totalII.value = infocarrera.value.II.listas + infocarrera.value.II.faltantes;
    return (totalII)
})

const realizadasII = computed(() => {
    const hecho = infocarrera.value.II.listas;
    const total = totalII.value;

    const listo = (hecho / total) * 100
    return Math.round(listo);
})

const evFaltantesII = computed(() => {
    const faltantes = infocarrera.value.II.faltantes;
    const total = totalII.value;

    const faltan = (faltantes / total) * 100
    return Math.round(faltan);
})

</script>


<template>
    <div class="flex flex-col items-center bg-[#ffdfab] w-full">
        <p class="text-xl text-black font-bold mb-10 mt-10">Evaluaciones por carreras</p>

        <div class="flex flex-col md:flex-row md:space-x-10 space-y-10 md:space-y-0">
            <button @click="openModal"
                class="bg-[#9fb9c2] text-white px-4 py-2 rounded-full w-52 h-52 flex flex-col justify-center items-center space-y-5">
                <img src="./ISC.png" alt="" class="w-16 h-16 ">
                <p class="text-white text-3xl font-bold">ISC</p>
            </button>

            <button @click="openModalIEM"
                class="bg-[#9fb9c2] text-white px-4 py-2 rounded-full w-52 h-52 flex flex-col justify-center items-center space-y-5">
                <img src="./IEM.png" alt="" class="w-16 h-16 ">
                <p class="text-white text-3xl font-bold">IEM</p>
            </button>

            <button @click="openModalIER"
                class="bg-[#9fb9c2] text-white px-4 py-2 rounded-full w-52 h-52 flex flex-col justify-center items-center space-y-5">
                <img src="./IER.png" alt="" class="w-16 h-16 ">
                <p class="text-white text-3xl font-bold">IER</p>
            </button>

            <button @click="openModalIE"
                class="bg-[#9fb9c2] text-white px-4 py-2 rounded-full w-52 h-52 flex flex-col justify-center items-center space-y-5">
                <img src="./IE.png" alt="" class="w-16 h-16 ">
                <p class="text-white text-3xl font-bold">IE</p>
            </button>

            <button @click="openModalII"
                class="bg-[#9fb9c2] text-white px-4 py-2 rounded-full w-52 h-52 flex flex-col justify-center items-center space-y-5">
                <img src="./II.png" alt="" class="w-16 h-16 ">
                <p class="text-white text-3xl font-bold">II</p>
            </button>
        </div>

        <!-- Ingeniería en Sistemas Computacionales -->
        <div v-if="Modal"
            class="bg-[#ffaa67] flex items-center justify-center md:w-[700px] h-[900px] w-[390px] flex-col md:translate-x-5 -translate-y-64">

            <button @click="closeModal" class="absolute top-0 right-0 m-2 bg-[#913f33] text-white px-4 py-2 rounded">
                <i class="fa-solid fa-xmark text-white text-2xl"></i>
            </button>

            <div class="space-y-5 flex flex-col justify-center items-center">
                <p class="md:text-3xl text-2xl text-white md:abolute md:-translate-y-12 translate-x-5 md:translate-x-0 font-bold">Ingeniería en Sistemas Computacionales</p>

                <div class="w-64 h-32 bg-[#913f33] flex justify-center items-center rounded-full flex-col">
                    <i class="fa-solid fa-user text-4xl text-white"></i>
                    <p class="text-xl text-white font-bold">Alumnos de ISC:</p>
                    <p class="text-xl text-white font-bold">{{ calcularTotalISC }}</p>
                </div>

                <div class="flex flex-col md:flex-row md:space-x-16 space-y-10 md:space-y-0">
                    <div class="w-64 h-32 bg-[#913f33] flex justify-center items-center rounded-full flex-col mt-5 md:mt-0">
                        <i class="fa-solid fa-user-check text-4xl text-white"></i>
                        <p class="text-xl text-white font-bold">Evaluaciones realizadas:</p>
                        <p class="text-xl text-white font-bold">{{ infocarrera.ISC.listas }}</p>
                    </div>

                    <div class="w-64 h-32 bg-[#913f33] flex justify-center items-center rounded-full flex-col">
                        <i class="fa-solid fa-user-xmark text-4xl text-white"></i>
                        <p class="text-xl text-white font-bold">Evaluaciones faltantes:</p>
                        <p class="text-xl text-white font-bold">{{ infocarrera.ISC.faltantes }}</p>
                    </div>
                </div>

            </div>

            <div class="bg-[#ff705f] md:w-[600px] md:h-[400px] w-[380px] h-[300px] mt-10 flex justify-center items-center">


                <div class="bg-[#ff705f] md:w-[500px] md:h-[300px] w-[350px] h-[250px] mt-10 border-l-4 border-b-4 border-black space-y-10">
                    <div class="mt-12">
                        <div class="md:h-14 h-10 bg-[#9fb9c2]" :style="{ 'widt': realizadasISC + '%' }">

                        </div>

                        <p class="text-xl text-black font-bold">Evaluaciones realizadas: {{ infocarrera.ISC.listas }} o {{
                            realizadasISC }} %</p>
                    </div>

                    <div>
                        <div class="md:h-14 h-10 bg-[#9fb9c2]" :style="{ 'width': evFaltantesISC + '%' }">

                        </div>

                        <p class="text-xl text-black font-bold">Evaluaciones faltantes: {{ infocarrera.ISC.faltantes }} o {{
                            evFaltantesISC }} %</p>
                    </div>

                </div>


            </div>
        </div>

        <!-- Ingeniería Electromecanica -->

        <div v-if="ModalIEM"
            class="bg-[#ffaa67] flex items-center justify-center md:w-[700px] h-[900px] w-[390px] flex-col md:translate-x-5 -translate-y-64">

            <button @click="closeModalIEM" class="absolute top-0 right-0 m-2 bg-[#913f33] text-white px-4 py-2 rounded">
                <i class="fa-solid fa-xmark text-white text-2xl"></i>
            </button>

            <div class="space-y-5 flex flex-col justify-center items-center">
                <p class="md:text-3xl text-2xl text-white md:abolute md:-translate-y-12 -translate-x-5 md:-translate-x-0 font-bold">Ingeniería Electromecánica</p>

                <div class="w-64 h-32 bg-[#913f33] flex justify-center items-center rounded-full flex-col">
                    <i class="fa-solid fa-user text-4xl text-white"></i>
                    <p class="text-xl text-white font-bold">Alumnos de IEM:</p>
                    <p class="text-xl text-white font-bold">{{ calcularTotalIEM }}</p>
                </div>

                <div class="flex flex-col md:flex-row md:space-x-16 space-y-10 md:space-y-0">
                    <div class="w-64 h-32 bg-[#913f33] flex justify-center items-center rounded-full flex-col mt-5 md:mt-0">
                        <i class="fa-solid fa-user-check text-4xl text-white"></i>
                        <p class="text-xl text-white font-bold">Evaluaciones realizadas:</p>
                        <p class="text-xl text-white font-bold">{{ infocarrera.IEM.listas }}</p>
                    </div>

                    <div class="w-64 h-32 bg-[#913f33] flex justify-center items-center rounded-full flex-col">
                        <i class="fa-solid fa-user-xmark text-4xl text-white"></i>
                        <p class="text-xl text-white font-bold">Evaluaciones faltantes:</p>
                        <p class="text-xl text-white font-bold">{{ infocarrera.IEM.faltantes }}</p>
                    </div>
                </div>

            </div>

            <div class="bg-[#ff705f] md:w-[600px] md:h-[400px] w-[380px] h-[300px] mt-10 flex justify-center items-center">


                <div class="bg-[#ff705f] md:w-[500px] md:h-[300px] w-[350px] h-[250px] mt-10 border-l-4 border-b-4 border-black space-y-10">
                    <div class="mt-12">
                        <div class="md:h-14 h-10 bg-[#9fb9c2]" :style="{ 'widt': realizadasIEM + '%' }">

                        </div>

                        <p class="text-xl text-black font-bold">Evaluaciones realizadas: {{ infocarrera.IEM.listas }} o {{
                            realizadasIEM }} %</p>
                    </div>

                    <div>
                        <div class="md:h-14 h-10 bg-[#9fb9c2]" :style="{ 'width': evFaltantesIEM + '%' }">

                        </div>

                        <p class="text-xl text-black font-bold">Evaluaciones faltantes: {{ infocarrera.IEM.faltantes }} o {{
                            evFaltantesIEM }} %</p>
                    </div>

                </div>


            </div>
        </div>

        <!-- Ingeniería en Energías renovables -->

        <div v-if="ModalIER"
            class="bg-[#ffaa67] flex items-center justify-center md:w-[700px] h-[900px] w-[390px] flex-col md:translate-x-5 -translate-y-64">

            <button @click="closeModalIER" class="absolute top-0 right-0 m-2 bg-[#913f33] text-white px-4 py-2 rounded">
                <i class="fa-solid fa-xmark text-white text-2xl"></i>
            </button>

            <div class="space-y-5 flex flex-col justify-center items-center">
                <p class="md:text-3xl text-2xl text-white md:abolute md:-translate-y-12 -translate-x-5 md:-translate-x-0 font-bold">Ingeniería en Energías <br class="md:hidden"> Renovables</p>

                <div class="w-64 h-32 bg-[#913f33] flex justify-center items-center rounded-full flex-col">
                    <i class="fa-solid fa-user text-4xl text-white"></i>
                    <p class="text-xl text-white font-bold">Alumnos de IER:</p>
                    <p class="text-xl text-white font-bold">{{ calcularTotalIER }}</p>
                </div>

                <div class="flex flex-col md:flex-row md:space-x-16 space-y-10 md:space-y-0">
                    <div class="w-64 h-32 bg-[#913f33] flex justify-center items-center rounded-full flex-col mt-5 md:mt-0">
                        <i class="fa-solid fa-user-check text-4xl text-white"></i>
                        <p class="text-xl text-white font-bold">Evaluaciones realizadas:</p>
                        <p class="text-xl text-white font-bold">{{ infocarrera.IER.listas }}</p>
                    </div>

                    <div class="w-64 h-32 bg-[#913f33] flex justify-center items-center rounded-full flex-col">
                        <i class="fa-solid fa-user-xmark text-4xl text-white"></i>
                        <p class="text-xl text-white font-bold">Evaluaciones faltantes:</p>
                        <p class="text-xl text-white font-bold">{{ infocarrera.IER.faltantes }}</p>
                    </div>
                </div>

            </div>

            <div class="bg-[#ff705f] md:w-[600px] md:h-[400px] w-[380px] h-[300px] mt-10 flex justify-center items-center">


                <div class="bg-[#ff705f] md:w-[500px] md:h-[300px] w-[350px] h-[250px] mt-10 border-l-4 border-b-4 border-black space-y-10">
                    <div class="mt-12">
                        <div class="md:h-14 h-10 bg-[#9fb9c2]" :style="{ 'widt': realizadasIER + '%' }">

                        </div>

                        <p class="text-xl text-black font-bold">Evaluaciones realizadas: {{ infocarrera.IER.listas }} o {{
                            realizadasIER }} %</p>
                    </div>

                    <div>
                        <div class="md:h-14 h-10 bg-[#9fb9c2]" :style="{ 'width': evFaltantesIER + '%' }">

                        </div>

                        <p class="text-xl text-black font-bold">Evaluaciones faltantes: {{ infocarrera.IER.faltantes }} o {{
                            evFaltantesIER }} %</p>
                    </div>

                </div>


            </div>
        </div>

        <!-- Ingeniería Electrónica -->

        <div v-if="ModalIE"
            class="bg-[#ffaa67] flex items-center justify-center md:w-[700px] h-[900px] w-[390px] flex-col md:translate-x-5 -translate-y-64">

            <button @click="closeModalIE" class="absolute top-0 right-0 m-2 bg-[#913f33] text-white px-4 py-2 rounded">
                <i class="fa-solid fa-xmark text-white text-2xl"></i>
            </button>

            <div class="space-y-5 flex flex-col justify-center items-center">
                <p class="md:text-3xl text-2xl text-white md:abolute md:-translate-y-12 -translate-x-5 md:-translate-x-0 font-bold">Ingeniería Electrónica</p>

                <div class="w-64 h-32 bg-[#913f33] flex justify-center items-center rounded-full flex-col">
                    <i class="fa-solid fa-user text-4xl text-white"></i>
                    <p class="text-xl text-white font-bold">Alumnos de IE:</p>
                    <p class="text-xl text-white font-bold">{{ calcularTotalIE }}</p>
                </div>

                <div class="flex flex-col md:flex-row md:space-x-16 space-y-10 md:space-y-0">
                    <div class="w-64 h-32 bg-[#913f33] flex justify-center items-center rounded-full flex-col mt-5 md:mt-0">
                        <i class="fa-solid fa-user-check text-4xl text-white"></i>
                        <p class="text-xl text-white font-bold">Evaluaciones realizadas:</p>
                        <p class="text-xl text-white font-bold">{{ infocarrera.IE.listas }}</p>
                    </div>

                    <div class="w-64 h-32 bg-[#913f33] flex justify-center items-center rounded-full flex-col">
                        <i class="fa-solid fa-user-xmark text-4xl text-white"></i>
                        <p class="text-xl text-white font-bold">Evaluaciones faltantes:</p>
                        <p class="text-xl text-white font-bold">{{ infocarrera.IE.faltantes }}</p>
                    </div>
                </div>

            </div>

            <div class="bg-[#ff705f] md:w-[600px] md:h-[400px] w-[380px] h-[300px] mt-10 flex justify-center items-center">


                <div class="bg-[#ff705f] md:w-[500px] md:h-[300px] w-[350px] h-[250px] mt-10 border-l-4 border-b-4 border-black space-y-10">
                    <div class="mt-12">
                        <div class="md:h-14 h-10 bg-[#9fb9c2]" :style="{ 'widt': realizadasIE + '%' }">

                        </div>

                        <p class="text-xl text-black font-bold">Evaluaciones realizadas: {{ infocarrera.IE.listas }} o {{
                            realizadasIE }} %</p>
                    </div>

                    <div>
                        <div class="md:h-14 h-10 bg-[#9fb9c2]" :style="{ 'width': evFaltantesIE + '%' }">

                        </div>

                        <p class="text-xl text-black font-bold">Evaluaciones faltantes: {{ infocarrera.IE.faltantes }} o {{
                            evFaltantesIE }} %</p>
                    </div>

                </div>


            </div>
        </div>

        <!-- Ingeniería Industrial -->

        <div v-if="ModalII"
            class="bg-[#ffaa67] flex items-center justify-center md:w-[700px] h-[900px] w-[390px] flex-col md:translate-x-5 -translate-y-64">

            <button @click="closeModalII" class="absolute top-0 right-0 m-2 bg-[#913f33] text-white px-4 py-2 rounded">
                <i class="fa-solid fa-xmark text-white text-2xl"></i>
            </button>

            <div class="space-y-5 flex flex-col justify-center items-center">
                <p class="md:text-3xl text-2xl text-white md:abolute md:-translate-y-12 -translate-x-5 md:-translate-x-0 font-bold">Ingeniería Industrial</p>

                <div class="w-64 h-32 bg-[#913f33] flex justify-center items-center rounded-full flex-col">
                    <i class="fa-solid fa-user text-4xl text-white"></i>
                    <p class="text-xl text-white font-bold">Alumnos de II:</p>
                    <p class="text-xl text-white font-bold">{{ calcularTotalII }}</p>
                </div>

                <div class="flex flex-col md:flex-row md:space-x-16 space-y-10 md:space-y-0">
                    <div class="w-64 h-32 bg-[#913f33] flex justify-center items-center rounded-full flex-col mt-5 md:mt-0">
                        <i class="fa-solid fa-user-check text-4xl text-white"></i>
                        <p class="text-xl text-white font-bold">Evaluaciones realizadas:</p>
                        <p class="text-xl text-white font-bold">{{ infocarrera.II.listas }}</p>
                    </div>

                    <div class="w-64 h-32 bg-[#913f33] flex justify-center items-center rounded-full flex-col">
                        <i class="fa-solid fa-user-xmark text-4xl text-white"></i>
                        <p class="text-xl text-white font-bold">Evaluaciones faltantes:</p>
                        <p class="text-xl text-white font-bold">{{ infocarrera.II.faltantes }}</p>
                    </div>
                </div>

            </div>

            <div class="bg-[#ff705f] md:w-[600px] md:h-[400px] w-[380px] h-[300px] mt-10 flex justify-center items-center">


                <div class="bg-[#ff705f] md:w-[500px] md:h-[300px] w-[350px] h-[250px] mt-10 border-l-4 border-b-4 border-black space-y-10">
                    <div class="mt-12">
                        <div class="md:h-14 h-10 bg-[#9fb9c2]" :style="{ 'widt': realizadasII + '%' }">

                        </div>

                        <p class="text-xl text-black font-bold">Evaluaciones realizadas: {{ infocarrera.II.listas }} o {{
                            realizadasII }} %</p>
                    </div>

                    <div>
                        <div class="md:h-14 h-10 bg-[#9fb9c2]" :style="{ 'width': evFaltantesII + '%' }">

                        </div>

                        <p class="text-xl text-black font-bold">Evaluaciones faltantes: {{ infocarrera.II.faltantes }} o {{
                            evFaltantesII }} %</p>
                    </div>

                </div>


            </div>
        </div>

    </div>
</template>