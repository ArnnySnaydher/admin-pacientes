<script setup>
import { ref,reactive } from 'vue';
import Header from './components/Header.vue';
import Formulario from './components/Formulario.vue';
import Paciente from './components/Paciente.vue'

const pacientes = ref([])

const paciente = reactive({
        nombre:'',
        propietario:'',
        email:'',
        alta:'',
        sintomas:''
    })

    const guardarPaciente = () =>{
      pacientes.value.push({...paciente})

      //Reiniciar objeto
      // paciente.nombre=''
      // paciente.propietario=''
      // paciente.email= ''
      // paciente.alta= ''
      // paciente.sintomas= ''

      //other
      Object.assign(paciente,{
        nombre:'',
        propietario:'',
        email:'',
        alta:'',
        sintomas:''
      })
    }
</script>

<template>
   <div class="container mx-auto mt-20 ">
    <Header></Header>

    <div class="mt-12 md:flex">
      <Formulario     
      v-model:nombre="paciente.nombre"
      v-model:propietario="paciente.propietario"
      v-model:email="paciente.email"
      v-model:alta="paciente.alta"
      v-model:sintomas="paciente.sintomas"
      @guardar-paciente="guardarPaciente">
      </Formulario>
      <div class="md:w-1/2 md:h-screen overflow-y-scroll">
        <h3 class="font-black text-3xl text-center">Administra tus Pacientes</h3>
        <div v-if="pacientes.length > 0">
          <p class="text-lg mt-5 text-center mb-10">
            Información de
            <span class="text-indigo-600 font-bold">Pacientes</span>
        </p>
        <Paciente v-for="paciente in pacientes" :paciente="paciente"></Paciente>
      </div>
        <p v-else="" class="mt-20 text-2xl text-center">No hay Pacientes</p>
      </div>
      
    </div>
   </div>
</template>


