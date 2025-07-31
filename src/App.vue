<template>
  <div>
    <RegisterView v-if="currentView === 'register'" @changeView="setCurrentView" />
    <LoginView v-if="currentView === 'login'" @login="loginUser" @changeView="setCurrentView" />
    <MenuView
      v-if="currentView === 'menu'"
      :user="user"
      @logout="logoutUser"
      @changeView="setCurrentView"
    />
    <FormView
      v-if="currentView === 'form'"
      :ubicaciones="ubicaciones"
      :formData="formData"
      @submitForm="submitForm"
      @updateFormData="updateFormData"
      @changeView="setCurrentView"
    />
    <HistorialView
      v-if="currentView === 'historial'"
      :historial="historialLimpiezas"
      @changeView="setCurrentView"
    />
  </div>
</template>

<script setup>
import { reactive, ref } from 'vue'
import RegisterView from './components/RegisterView.vue'
import LoginView from './components/LoginView.vue'
import MenuView from './components/MenuView.vue'
import FormView from './components/FormView.vue'
import HistorialView from './components/HistorialView.vue'

const currentView = ref('register')
const user = ref(null)
const historialLimpiezas = ref([])

const formData = reactive({
  fecha: new Date().toISOString().split('T')[0],
  hora: new Date().toTimeString().split(' ')[0].slice(0, 5),
  tipoLimpieza: '',
  reposicion: {
    papel: false,
    toalla: false,
    jabon: false,
  },
  bloque: '',
  tipoLugar: '',
  lugar: '',
  observaciones: '',
})

const ubicaciones = {
  'bloque-9': {
    nombre: 'Bloque 9 - Edificio de Postgrado UPB',
    tiposLugar: {
      bano: {
        nombre: 'Baño',
        lugares: [
          'Piso 1 - Damas',
          'Piso 1 - Caballeros',
          'Piso 2 - Damas',
          'Piso 2 - Caballeros',
          'Piso 3 - Damas',
          'Piso 3 - Caballeros',
        ],
      },
      aula: {
        nombre: 'Aula',
        lugares: [
          'Aula 101',
          'Aula 102',
          'Aula 201',
          'Aula 202',
          'Aula 301',
          'Laboratorio de Cómputo',
        ],
      },
      oficina: {
        nombre: 'Oficina',
        lugares: ['Secretaría', 'Decanatura', 'Coordinación', 'Sala de Profesores'],
      },
    },
  },
  'bloque-8': {
    nombre: 'Bloque 8 - Biblioteca',
    tiposLugar: {
      sala: {
        nombre: 'Sala',
        lugares: [
          'Sala de Lectura Piso 1',
          'Sala de Lectura Piso 2',
          'Sala de Estudio Grupal',
          'Sala de Computadores',
        ],
      },
      bano: {
        nombre: 'Baño',
        lugares: ['Piso 1 - Damas', 'Piso 1 - Caballeros', 'Piso 2 - Damas', 'Piso 2 - Caballeros'],
      },
    },
  },
}

function setCurrentView(view) {
  currentView.value = view
}

function loginUser(usuario) {
  user.value = usuario
  currentView.value = 'menu'
}

function logoutUser() {
  user.value = null
  currentView.value = 'login'
}

function submitForm() {
  historialLimpiezas.value.push({
    id: Date.now(),
    ...JSON.parse(JSON.stringify(formData)),
    usuario: user.value.name,
  })
  Object.assign(formData, {
    fecha: new Date().toISOString().split('T')[0],
    hora: new Date().toTimeString().split(' ')[0].slice(0, 5),
    tipoLimpieza: '',
    reposicion: { papel: false, toalla: false, jabon: false },
    bloque: '',
    tipoLugar: '',
    lugar: '',
    observaciones: '',
  })
  currentView.value = 'menu'
}

function updateFormData(field, value) {
  if (field in formData) {
    formData[field] = value
  }
}

function agregarRegistro(nuevo) {
  historial.value.push(nuevo);
}

</script>

<style scoped>
body {
  font-family: 'Inter', sans-serif;
}
/* Estilos del Contenedor Principal */
.min-h-screen {
  min-height: 100vh;
}

.from-blue-50 {
  --tw-gradient-from: #eff6ff;
  --tw-gradient-stops: var(--tw-gradient-from), var(--tw-gradient-to, rgba(239, 246, 255, 0));
}

.to-green-50 {
  --tw-gradient-to: #f0fdf4;
}

.flex {
  display: flex;
}

.items-center {
  align-items: center;
}

.justify-center {
  justify-content: center;
}

.p-4 {
  padding: 1rem;
}

/* Estilos de la Tarjeta */
.bg-white {
  background-color: #fff;
}

.rounded-2xl {
  border-radius: 1rem;
}

.shadow-xl {
  box-shadow:
    0 20px 25px -5px rgba(0, 0, 0, 0.1),
    0 10px 10px -5px rgba(0, 0, 0, 0.04);
}

.p-8 {
  padding: 2rem;
}

.w-full {
  width: 100%;
}

.max-w-md {
  max-width: 28rem;
}

/* Estilos del Encabezado */
.text-center {
  text-align: center;
}

.mb-8 {
  margin-bottom: 2rem;
}

.w-16 {
  width: 4rem;
}

.h-16 {
  height: 4rem;
}

.bg-green-100 {
  background-color: #d1fae5;
}

.rounded-full {
  border-radius: 9999px;
}

.mx-auto {
  margin-left: auto;
  margin-right: auto;
}

.mb-4 {
  margin-bottom: 1rem;
}

.w-8 {
  width: 2rem;
}

.h-8 {
  height: 2rem;
}

.text-green-600 {
  color: #059669;
}

.text-2xl {
  font-size: 1.5rem;
  line-height: 2rem;
}

.font-bold {
  font-weight: 700;
}

.text-gray-400 {
  color: #9ca3af;
}

/* Estilos del Formulario */
.space-y-4 > :not([hidden]) ~ :not([hidden]) {
  --tw-space-y-reverse: 0;
  margin-top: calc(1rem * calc(1 - var(--tw-space-y-reverse)));
  margin-bottom: calc(1rem * var(--tw-space-y-reverse));
}

.grid {
  display: grid;
}

.grid-cols-2 {
  grid-template-columns: repeat(2, minmax(0, 1fr));
}

.gap-4 {
  gap: 1rem;
}

.block {
  display: block;
}

.text-sm {
  font-size: 0.875rem;
  line-height: 1.25rem;
}

.font-medium {
  font-weight: 500;
}

.text-gray-700 {
  color: #374151;
}

.mb-1 {
  margin-bottom: 0.25rem;
}

.w-full {
  width: 100%;
}

.px-3 {
  padding-left: 0.75rem;
  padding-right: 0.75rem;
}

.py-2 {
  padding-top: 0.5rem;
  padding-bottom: 0.5rem;
}

.border {
  border-width: 1px;
}

.border-gray-300 {
  border-color: #d1d5db;
}

.rounded-lg {
  border-radius: 0.5rem;
}

.focusring-2:focus {
  --tw-ring-offset-shadow: var(--tw-ring-inset) 0 0 0 var(--tw-ring-offset-width)
    var(--tw-ring-offset-color);
  --tw-ring-shadow: var(--tw-ring-inset) 0 0 0 calc(2px + var(--tw-ring-offset-width))
    var(--tw-ring-color);
  box-shadow: var(--tw-ring-offset-shadow), var(--tw-ring-shadow), var(--tw-shadow, 0 0 #0000);
}

.focusring-blue-500:focus {
  --tw-ring-color: #3b82f6;
}

.focusborder-transparent:focus {
  border-color: transparent;
}

.flex {
  display: flex;
}

.gap-2 {
  gap: 0.5rem;
}

.flex-1 {
  flex: 1 1 0%;
}

/* Estilos del Botón de Registrar */
.bg-blue-600 {
  background-color: #2563eb;
}

.text-white {
  color: #fff;
}

.py-3 {
  padding-top: 0.75rem;
  padding-bottom: 0.75rem;
}

.hoverbg-blue-700:hover {
  background-color: #1d4ed8;
}

.transition {
  transition-property:
    color,
    background-color,
    border-color,
    text-decoration-color,
    fill,
    stroke,
    opacity,
    box-shadow,
    transform,
    filter,
    -webkit-backdrop-filter;
  transition-property:
    color, background-color, border-color, text-decoration-color, fill, stroke, opacity, box-shadow,
    transform, filter, backdrop-filter;
  transition-property:
    color,
    background-color,
    border-color,
    text-decoration-color,
    fill,
    stroke,
    opacity,
    box-shadow,
    transform,
    filter,
    backdrop-filter,
    -webkit-backdrop-filter;
  transition-timing-function: cubic-bezier(0.4, 0, 0.2, 1);
  transition-duration: 150ms;
}

.duration-200 {
  transition-duration: 200ms;
}

/* Estilos del Pie de página */
.text-center {
  text-align: center;
}

.text-sm {
  font-size: 0.875rem;
  line-height: 1.25rem;
}

.text-gray-600 {
  color: #4b5563;
}

.mt-4 {
  margin-top: 1rem;
}

.text-blue-600 {
  color: #2563eb;
}

.hoverunderline:hover {
  text-decoration-line: underline;
}
</style>
