<template>
  <div
    class="min-h-screen bg-gradient-to-br from-blue-50 to-green-50 flex items-center justify-center p-4"
  >
    <div class="bg-white rounded-2xl shadow-xl p-8 w-full max-w-md">
      <div class="text-center mb-8">
        <div
          class="w-16 h-16 bg-blue-100 rounded-full flex items-center justify-center mx-auto mb-4"
        >
          <LockKeyhole class="w-8 h-8 text-blue-600" />
        </div>
        <h1 class="text-2xl font-bold text-gray-800">Iniciar sesión</h1>
      </div>

      <form class="space-y-4" @submit.prevent="$emit('changeView', 'menu')">
        <div>
          <label class="block text-sm font-medium text-gray-700 mb-1">Cedula</label>
          <input
            type="text"
            placeholder="1111111111"
            class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent"
            required
          />
        </div>

        <div>
          <label class="block text-sm font-medium text-gray-700 mb-1">Contraseña</label>
          <input
            type="password"
            placeholder="••••••••"
            class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent"
            required
          />
        </div>

        <button
          type="submit"
          class="w-full bg-blue-600 text-white py-3 rounded-lg hover:bg-blue-700 transition duration-200 font-medium"
        >
          Iniciar sesión →
        </button>
      </form>

      <p class="text-center text-sm text-gray-600 mt-4">
        ¿No tienes cuenta?
        <button @click="$emit('changeView', 'register')" class="text-blue-600 hover:underline">
          Regístrate
        </button>
      </p>
    </div>
  </div>
</template>

<script setup>
import { LockKeyhole } from 'lucide-vue-next'
</script>
