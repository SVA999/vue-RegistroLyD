<template>
  <div
    class="min-h-screen bg-gradient-to-br from-blue-50 to-green-50 flex items-center justify-center p-4"
  >
    <div class="bg-white rounded-2xl shadow-xl p-8 w-full max-w-md text-center space-y-6">
      <div class="w-16 h-16 bg-indigo-100 rounded-full flex items-center justify-center mx-auto">
        <LayoutGrid class="w-8 h-8 text-indigo-600" />
      </div>
      <h1 class="text-2xl font-bold text-gray-800">Menú principal</h1>
      <div class="space-y-4">
        <button
          @click="$emit('changeView', 'form')"
          class="w-full bg-green-500 text-white py-3 rounded-lg hover:bg-green-600 transition duration-200 font-medium"
        >
          📝 Llenar formulario
        </button>
        <button
          @click="$emit('changeView', 'historial')"
          class="w-full bg-blue-500 text-white py-3 rounded-lg hover:bg-blue-600 transition duration-200 font-medium"
        >
          📄 Ver historial
        </button>
        <button
          @click="$emit('changeView', 'login')"
          class="w-full bg-red-500 text-white py-3 rounded-lg hover:bg-red-600 transition duration-200 font-medium"
        >
          🚪 Cerrar sesión
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { LayoutGrid } from 'lucide-vue-next'
</script>
