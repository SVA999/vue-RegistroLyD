<template>
  <div class="container">
    <div class="header">
      <div class="logo">UPB</div>
      <div class="header-text">
        <h1>Registrar limpieza</h1>
        <p>{{ formattedDate }} - {{ formattedTime }}</p>
      </div>
    </div>

    <div class="form-container">
      <form @submit.prevent="submitForm">
        <!-- Tipo de aseo -->
        <div class="form-group">
          <div class="section-title"><span>⚫</span> Tipo de aseo</div>
          <div class="radio-group">
            <div class="radio-option">
              <input
                type="radio"
                id="general"
                name="tipoLimpieza"
                value="general"
                v-model="formData.tipoLimpieza"
              />
              <label for="general">General</label>
            </div>
            <div class="radio-option">
              <input
                type="radio"
                id="profundo"
                name="tipoLimpieza"
                value="profundo"
                v-model="formData.tipoLimpieza"
              />
              <label for="profundo">Profundo</label>
            </div>
            <div class="radio-option">
              <input
                type="radio"
                id="desinfeccion"
                name="tipoLimpieza"
                value="desinfeccion"
                v-model="formData.tipoLimpieza"
              />
              <label for="desinfeccion">Desinfección</label>
            </div>
          </div>
        </div>

        <!-- Reposición de elementos -->
        <div class="form-group">
          <div class="section-title">Reposición de elementos</div>
          <div class="checkbox-group">
            <div class="checkbox-option">
              <input type="checkbox" id="papel" v-model="formData.reposicion.papel" />
              <label for="papel">Papel</label>
            </div>
            <div class="checkbox-option">
              <input type="checkbox" id="toalla" v-model="formData.reposicion.toalla" />
              <label for="toalla">Toalla</label>
            </div>
            <div class="checkbox-option">
              <input type="checkbox" id="jabon" v-model="formData.reposicion.jabon" />
              <label for="jabon">Jabón</label>
            </div>
          </div>
        </div>

        <!-- Bloque -->
        <div class="form-group">
          <label class="form-label">Bloque</label>
          <div class="select-container">
            <select v-model="formData.bloque" class="form-select">
              <option value="">Bloque 9 - Edificio de Posgrados UPB</option>
              <option v-for="(bloque, key) in ubicaciones" :key="key" :value="key">
                {{ bloque.nombre }}
              </option>
            </select>
          </div>
        </div>

        <!-- Tipo lugar -->
        <div class="form-group" v-if="formData.bloque">
          <label class="form-label">Tipo lugar</label>
          <div class="select-container">
            <select v-model="formData.tipoLugar" class="form-select">
              <option value="">Baño</option>
              <option
                v-for="(tipo, key) in ubicaciones[formData.bloque].tiposLugar"
                :key="key"
                :value="key"
              >
                {{ tipo.nombre }}
              </option>
            </select>
          </div>
        </div>

        <!-- Lugar -->
        <div class="form-group" v-if="formData.bloque && formData.tipoLugar">
          <label class="form-label">Lugar</label>
          <div class="select-container">
            <select v-model="formData.lugar" class="form-select">
              <option value="">Piso 2 - Caballeros</option>
              <option
                v-for="(lugar, index) in ubicaciones[formData.bloque].tiposLugar[formData.tipoLugar]
                  .lugares"
                :key="index"
                :value="lugar"
              >
                {{ lugar }}
              </option>
            </select>
          </div>
        </div>

        <!-- Observaciones -->
        <div class="form-group">
          <label class="form-label">⚫ Observaciones</label>
          <textarea
            v-model="formData.observaciones"
            class="form-textarea"
            placeholder="Por aquí tus observaciones en esta limpieza..."
          ></textarea>
        </div>

        <!-- Botón submit -->
        <button type="submit" :disabled="!isFormValid" class="submit-btn">
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
  tipoLimpieza: 'general',
  reposicion: { papel: true, toalla: false, jabon: true },
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
  return formData.value.tipoLimpieza
})

const formattedDate = new Date().toLocaleDateString('es-ES')
const formattedTime = new Date().toLocaleTimeString('es-ES', {
  hour: '2-digit',
  minute: '2-digit',
})

function submitForm() {
  alert('Formulario enviado con éxito')
  emit('changeView', 'menu')
}
</script>

<style scoped>
.container {
  max-width: 400px;
  margin: 0 auto;
  background: white;
  border-radius: 12px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  overflow: hidden;
}

.header {
  display: flex;
  align-items: center;
  gap: 12px;
  padding: 20px;
  border-bottom: 1px solid #e9ecef;
}

.logo {
  width: 40px;
  height: 40px;
  background: #28a745;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  font-weight: bold;
  font-size: 18px;
}

.header-text h1 {
  font-size: 18px;
  font-weight: 600;
  color: #333;
  margin-bottom: 2px;
}

.header-text p {
  font-size: 12px;
  color: #666;
}

.form-container {
  padding: 20px;
}

.form-group {
  margin-bottom: 20px;
}

.form-label {
  display: block;
  font-size: 14px;
  font-weight: 500;
  color: #333;
  margin-bottom: 8px;
}

.radio-group {
  display: flex;
  gap: 8px;
  margin-bottom: 16px;
}

.radio-option {
  display: flex;
  align-items: center;
  gap: 8px;
  cursor: pointer;
}

.radio-option input[type='radio'] {
  margin: 0;
}

.radio-option label {
  font-size: 14px;
  color: #333;
  cursor: pointer;
}

.checkbox-group {
  display: flex;
  gap: 16px;
  margin-bottom: 16px;
}

.checkbox-option {
  display: flex;
  align-items: center;
  gap: 8px;
  cursor: pointer;
}

.checkbox-option input[type='checkbox'] {
  margin: 0;
}

.checkbox-option label {
  font-size: 14px;
  color: #333;
  cursor: pointer;
}

.select-container {
  position: relative;
  margin-bottom: 12px;
}

.form-select {
  width: 100%;
  padding: 12px;
  border: 1px solid #ddd;
  border-radius: 8px;
  font-size: 14px;
  background: white;
  appearance: none;
  background-image: url("data:image/svg+xml,%3csvg xmlns='http://www.w3.org/2000/svg' fill='none' viewBox='0 0 20 20'%3e%3cpath stroke='%236b7280' stroke-linecap='round' stroke-linejoin='round' stroke-width='1.5' d='M6 8l4 4 4-4'/%3e%3c/svg%3e");
  background-position: right 12px center;
  background-repeat: no-repeat;
  background-size: 16px;
  padding-right: 40px;
}

.form-select:focus {
  outline: none;
  border-color: #007bff;
  box-shadow: 0 0 0 2px rgba(0, 123, 255, 0.25);
}

.form-textarea {
  width: 100%;
  padding: 12px;
  border: 1px solid #ddd;
  border-radius: 8px;
  font-size: 14px;
  font-family: inherit;
  resize: vertical;
  min-height: 80px;
}

.form-textarea:focus {
  outline: none;
  border-color: #007bff;
  box-shadow: 0 0 0 2px rgba(0, 123, 255, 0.25);
}

.form-textarea::placeholder {
  color: #999;
}

.submit-btn {
  width: 100%;
  padding: 12px;
  background: #007bff;
  color: white;
  border: none;
  border-radius: 8px;
  font-size: 14px;
  font-weight: 500;
  cursor: pointer;
  transition: background-color 0.2s;
}

.submit-btn:hover:not(:disabled) {
  background: #0056b3;
}

.submit-btn:disabled {
  background: #ccc;
  cursor: not-allowed;
}

.section-title {
  font-size: 14px;
  font-weight: 500;
  color: #333;
  margin-bottom: 12px;
  display: flex;
  align-items: center;
  gap: 6px;
}
</style>
