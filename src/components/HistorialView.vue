<template>
  <div class="min-h-screen bg-gradient-to-br from-blue-50 to-green-50 flex items-center justify-center p-4">
    <div class="bg-white rounded-2xl shadow-xl p-6 w-full max-w-2xl">
      <div class="flex items-center justify-between mb-6">
        <div class="flex items-center space-x-3">
          <ScrollText class="w-8 h-8 text-indigo-600" />
          <h1 class="text-xl font-bold text-gray-800">Historial de registros</h1>
        </div>
        <button @click="$emit('changeView', 'menu')" class="text-blue-600 hover:underline">
          ← Volver
        </button>
      </div>

      <ul class="space-y-4 max-h-[65vh] overflow-y-auto pr-2">
        <li
          v-for="(item, index) in historial"
          :key="index"
          class="border border-gray-200 rounded-lg p-4 shadow-sm hover:shadow-md transition duration-200 bg-white"
        >
          <p class="text-sm text-gray-600 mb-1">📅 {{ item.fecha }} - 🕒 {{ item.hora }}</p>
          <p class="font-semibold text-gray-800">🧹 Tipo de limpieza: {{ capitalize(item.tipoLimpieza) }}</p>
          <p class="text-sm text-gray-700">📍 Zona: {{ item.bloque }} > {{ item.tipoLugar }} > {{ item.lugar }}</p>

          <div v-if="hasReposicion(item.reposicion)" class="mt-1 text-sm text-gray-700">
            📦 Reposición: 
            <span v-if="item.reposicion.papel">Papel</span>
            <span v-if="item.reposicion.toalla"> | Toalla</span>
            <span v-if="item.reposicion.jabon"> | Jabón</span>
          </div>

          <p class="text-sm text-gray-500 italic mt-1" v-if="item.observaciones">🗒 {{ item.observaciones }}</p>
        </li>
      </ul>
    </div>
  </div>
</template>

<script setup>
import { ScrollText } from 'lucide-vue-next';

// Datos de ejemplo (debes reemplazarlos con fuente real de datos o store global)
const historial = [
  {
    fecha: '2025-07-31',
    hora: '10:32',
    tipoLimpieza: 'general',
    bloque: 'Bloque 3',
    tipoLugar: 'Baños',
    lugar: 'Baño mujeres - piso 2',
    reposicion: {
      papel: true,
      toalla: false,
      jabon: true,
    },
    observaciones: 'Basurero lleno y piso mojado al inicio.',
  },
  {
    fecha: '2025-07-30',
    hora: '15:05',
    tipoLimpieza: 'desinfección',
    bloque: 'Bloque 2',
    tipoLugar: 'Aulas',
    lugar: 'Aula 205',
    reposicion: {
      papel: false,
      toalla: false,
      jabon: false,
    },
    observaciones: '',
  },
];

const capitalize = (text) => text.charAt(0).toUpperCase() + text.slice(1);
const hasReposicion = (repo) => repo.papel || repo.toalla || repo.jabon;
</script>
