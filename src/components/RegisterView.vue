<template>
  <div
    class="min-h-screen bg-gradient-to-br from-blue-50 to-green-50 flex items-center justify-center p-4"
  >
    <div class="bg-white rounded-2xl shadow-xl p-8 w-full max-w-md">
      <div class="text-center mb-8">
        <div
          class="w-16 h-16 bg-green-100 rounded-full flex items-center justify-center mx-auto mb-4"
        >
          <Users class="w-8 h-8 text-green-600" />
        </div>
        <h1 class="text-2xl font-bold text-gray-800">Registro</h1>
      </div>

      <form class="space-y-4" @submit.prevent="$emit('changeView', 'login')">
        <div class="grid grid-cols-2 gap-4">
          <div>
            <label class="block text-sm font-medium text-gray-700 mb-1">Nombre completo</label>
            <input
              type="text"
              placeholder="Jessica"
              class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent"
              required
            />
          </div>
          <div>
            <label class="block text-sm font-medium text-gray-700 mb-1">Apellido</label>
            <input
              type="text"
              placeholder="Alvarez"
              class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent"
              required
            />
          </div>
        </div>

        <div>
          <label class="block text-sm font-medium text-gray-700 mb-1">Documento de identidad</label>
          <div class="flex gap-2">
            <select
              class="px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500"
            >
              <option>CC</option>
              <option>TI</option>
              <option>CE</option>
            </select>
            <input
              type="text"
              placeholder="1011515455"
              class="flex-1 px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent"
              required
            />
          </div>
        </div>

        <div>
          <label class="block text-sm font-medium text-gray-700 mb-1">Teléfono</label>
          <div class="flex gap-2">
            <select
              class="px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500"
            >
              <option>🇨🇴 +57</option>
            </select>
            <input
              type="tel"
              placeholder="Número de teléfono"
              class="flex-1 px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent"
              required
            />
          </div>
        </div>

        <div>
          <label class="block text-sm font-medium text-gray-700 mb-1">Sector</label>
          <select
            class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500"
          >
            <option>🎓 Educativo</option>
            <option>🏢 Corporativo</option>
            <option>🏥 Salud</option>
          </select>
        </div>

        <div>
          <label class="block text-sm font-medium text-gray-700 mb-1">Ubicación</label>
          <select
            class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500"
          >
            <option>📍 Universidad Pontificia Bolivariana</option>
          </select>
        </div>

        <div>
          <label class="block text-sm font-medium text-gray-700 mb-1">Área</label>
          <select
            class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500"
          >
            <option>🧹 Limpieza</option>
            <option>🔧 Mantenimiento</option>
            <option>🛡️ Seguridad</option>
          </select>
        </div>

        <button
          type="submit"
          class="w-full bg-blue-600 text-white py-3 rounded-lg hover:bg-blue-700 transition duration-200 font-medium"
        >
          Registrar →
        </button>
      </form>

      <p class="text-center text-sm text-gray-600 mt-4">
        ¿Ya tienes cuenta?
        <button @click="$emit('changeView', 'login')" class="text-blue-600 hover:underline">
          Iniciar sesión
        </button>
      </p>
    </div>
  </div>
</template>

<script setup>
import { Users } from 'lucide-vue-next'
</script>
