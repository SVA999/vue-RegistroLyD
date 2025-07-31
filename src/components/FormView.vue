<template>
  <div
    class="min-h-screen bg-gradient-to-br from-blue-50 to-green-50 flex items-center justify-center p-4"
  >
    <div class="bg-white rounded-2xl shadow-xl p-8 w-full max-w-2xl">
      <div class="flex items-center justify-between mb-6">
        <div class="flex items-center gap-3">
          <div class="w-12 h-12 bg-white rounded-full flex items-center justify-center">
            <img
              src="https://upload.wikimedia.org/wikipedia/commons/thumb/1/15/Universidad_Pontificia_Bolivariana_logo.svg/1200px-Universidad_Pontificia_Bolivariana_logo.svg.png"
              alt="Logo UPB"
              class="w-full h-full object-contain"
            />
          </div>
          <div>
            <h1 class="text-xl font-bold text-gray-800">Registrar limpieza</h1>
            <p class="text-xs text-gray-600">{{ formattedDate }} - {{ formattedTime }}</p>
          </div>
        </div>
        <button
          @click="$emit('changeView', 'menu')"
          class="text-gray-500 hover:text-gray-700 text-2xl font-bold"
        >
          ✕
        </button>
      </div>

      <form @submit.prevent="submitForm" class="space-y-4">
        <div>
          <label class="block text-sm font-medium text-gray-700 mb-2"> 🧹 Tipo de aseo </label>
          <div class="grid grid-cols-1 sm:grid-cols-3 gap-3">
            <label
              v-for="tipo in ['general', 'profundo', 'desinfección']"
              :key="tipo"
              :class="{
                'border-blue-500 ring-2 ring-blue-500': formData.tipoLimpieza === tipo,
              }"
              class="flex items-center gap-3 p-4 border rounded-lg hover:bg-gray-50 cursor-pointer transition duration-200 text-sm bg-white shadow-sm"
            >
              <input
                type="radio"
                name="tipoLimpieza"
                :value="tipo"
                v-model="formData.tipoLimpieza"
                class="w-4 h-4 text-blue-600"
              />
              <span class="capitalize">{{ tipo }}</span>
            </label>
          </div>
        </div>

        <div>
          <label class="block text-sm font-medium text-gray-700 mb-2">
            📦 Reposición de elementos
          </label>
          <div class="grid grid-cols-1 sm:grid-cols-3 gap-3">
            <label
              v-for="item in [
                { key: 'papel', label: 'Papel' },
                { key: 'toalla', label: 'Toalla' },
                { key: 'jabon', label: 'Jabón' },
              ]"
              :key="item.key"
              :class="{
                'border-blue-500 ring-2 ring-blue-500': formData.reposicion[item.key],
              }"
              class="flex items-center gap-3 p-4 border rounded-lg hover:bg-gray-50 cursor-pointer transition duration-200 text-sm bg-white shadow-sm"
            >
              <input
                type="checkbox"
                v-model="formData.reposicion[item.key]"
                class="w-4 h-4 text-blue-600 rounded"
              />
              <span>{{ item.label }}</span>
            </label>
          </div>
        </div>

        <div>
          <label class="block text-sm font-medium text-gray-700 mb-2"> 📍 Lugar </label>
          <div class="space-y-2">
            <div>
              <label class="block text-xs text-gray-600 mb-1">Bloque</label>
              <select
                v-model="formData.bloque"
                class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 text-sm"
              >
                <option value="">Seleccionar bloque</option>
                <option v-for="(bloque, key) in ubicaciones" :key="key" :value="key">
                  {{ bloque.nombre }}
                </option>
              </select>
            </div>
            <div v-if="formData.bloque">
              <label class="block text-xs text-gray-600 mb-1">Tipo de lugar</label>
              <select
                v-model="formData.tipoLugar"
                class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 text-sm"
              >
                <option value="">Seleccionar tipo</option>
                <option
                  v-for="(tipo, key) in ubicaciones[formData.bloque].tiposLugar"
                  :key="key"
                  :value="key"
                >
                  {{ tipo.nombre }}
                </option>
              </select>
            </div>
            <div v-if="formData.bloque && formData.tipoLugar">
              <label class="block text-xs text-gray-600 mb-1">Lugar</label>
              <select
                v-model="formData.lugar"
                class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 text-sm"
              >
                <option value="">Seleccionar lugar</option>
                <option
                  v-for="(lugar, index) in ubicaciones[formData.bloque].tiposLugar[
                    formData.tipoLugar
                  ].lugares"
                  :key="index"
                  :value="lugar"
                >
                  {{ lugar }}
                </option>
              </select>
            </div>
          </div>
        </div>

        <div>
          <label class="block text-sm font-medium text-gray-700 mb-2"> 📝 Observaciones </label>
          <textarea
            v-model="formData.observaciones"
            rows="3"
            placeholder="Por aquí tus observaciones en esta limpieza..."
            class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent resize-none text-sm"
          ></textarea>
        </div>

        <button
          type="submit"
          :disabled="!isFormValid"
          class="w-full bg-blue-600 text-white py-3 rounded-lg hover:bg-blue-700 transition duration-200 font-medium disabled:bg-gray-300 disabled:cursor-not-allowed flex items-center justify-center gap-2 text-sm"
        >
          ✓ Registrar limpieza >
        </button>
      </form>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

const emit = defineEmits(['changeView'])

const formData = ref({
  tipoLimpieza: '',
  reposicion: { papel: false, toalla: false, jabon: false },
  bloque: '',
  tipoLugar: '',
  lugar: '',
  observaciones: '',
})

const ubicaciones = {
  A: {
    nombre: 'Bloque A',
    tiposLugar: {
      aulas: { nombre: 'Aulas', lugares: ['101', '102', '103'] },
      banos: { nombre: 'Baños', lugares: ['Baño 1', 'Baño 2'] },
    },
  },
  B: {
    nombre: 'Bloque B',
    tiposLugar: {
      oficinas: { nombre: 'Oficinas', lugares: ['Admin', 'Coordinación'] },
    },
  },
}

const isFormValid = computed(() => {
  return (
    formData.value.tipoLimpieza &&
    formData.value.bloque &&
    formData.value.tipoLugar &&
    formData.value.lugar
  )
})

const formattedDate = new Date().toLocaleDateString()
const formattedTime = new Date().toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' })

function submitForm() {
  alert('Formulario enviado con éxito')
  emit('changeView', 'menu')
}
</script>
