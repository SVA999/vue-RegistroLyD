<template>
  <div class="container">
    <div class="header">
      <div class="logo">UPB</div>
      <h1>Registro</h1>
    </div>

    <div class="form-container">
      <form @submit.prevent="submitForm">
        <!-- Nombre y Apellido -->
        <div class="form-row">
          <div class="form-group">
            <label class="form-label">Nombre completo</label>
            <input
              type="text"
              v-model="formData.nombre"
              placeholder="Jessica"
              class="form-input"
              required
            />
          </div>
          <div class="form-group">
            <label class="form-label">Apellido</label>
            <input
              type="text"
              v-model="formData.apellido"
              placeholder="Alvarez"
              class="form-input"
              required
            />
          </div>
        </div>

        <!-- Documento de identidad -->
        <div class="form-group">
          <label class="form-label">Documento de identidad</label>
          <div class="input-group">
            <select v-model="formData.tipoDocumento" class="form-select-small">
              <option value="CC">CC</option>
              <option value="TI">TI</option>
              <option value="CE">CE</option>
            </select>
            <input
              type="text"
              v-model="formData.documento"
              placeholder="1011515455"
              class="form-input-flex"
              required
            />
          </div>
        </div>

        <!-- Teléfono -->
        <div class="form-group">
          <label class="form-label">Phone number</label>
          <div class="input-group">
            <select class="form-select-small">
              <option value="+57">🇨🇴 +57</option>
            </select>
            <input
              type="tel"
              v-model="formData.telefono"
              placeholder="Phone number"
              class="form-input-flex"
              required
            />
          </div>
        </div>

        <!-- Sector -->
        <div class="form-group">
          <label class="form-label">Sector</label>
          <select v-model="formData.sector" class="form-select">
            <option value="educativo">🎓 Educativo</option>
            <option value="corporativo">🏢 Corporativo</option>
            <option value="salud">🏥 Salud</option>
          </select>
        </div>

        <!-- Ubicación -->
        <div class="form-group">
          <label class="form-label">Ubicación</label>
          <select v-model="formData.ubicacion" class="form-select">
            <option value="upb">📍 Universidad Pontificia Bolivariana</option>
          </select>
        </div>

        <!-- Área -->
        <div class="form-group">
          <label class="form-label">Área</label>
          <select v-model="formData.area" class="form-select">
            <option value="limpieza">🧹 Limpieza</option>
            <option value="mantenimiento">🔧 Mantenimiento</option>
            <option value="seguridad">🛡️ Seguridad</option>
          </select>
        </div>

        <!-- Botón submit -->
        <button type="submit" class="submit-btn">Registrar ></button>
      </form>

      <!-- Link a login -->
      <div class="login-link">
        <span>¿Ya tienes cuenta?</span>
        <button @click="goToLogin" class="link-button">Iniciar sesión</button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const emit = defineEmits(['changeView'])

const formData = ref({
  nombre: '',
  apellido: '',
  tipoDocumento: 'CC',
  documento: '',
  telefono: '',
  sector: 'educativo',
  ubicacion: 'upb',
  area: 'limpieza',
})

function submitForm() {
  console.log('Datos de registro:', formData.value)
  alert('Registro exitoso!')
  emit('changeView', 'login')
}

function goToLogin() {
  emit('changeView', 'login')
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
  text-align: center;
  padding: 30px 20px 20px;
  border-bottom: 1px solid #e9ecef;
}

.logo {
  width: 50px;
  height: 50px;
  background: #28a745;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  font-weight: bold;
  font-size: 20px;
  margin: 0 auto 15px;
}

.header h1 {
  font-size: 24px;
  font-weight: 600;
  color: #333;
  margin: 0;
}

.form-container {
  padding: 20px;
}

.form-row {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 12px;
  margin-bottom: 16px;
}

.form-group {
  margin-bottom: 16px;
}

.form-label {
  display: block;
  font-size: 14px;
  font-weight: 500;
  color: #333;
  margin-bottom: 6px;
}

.form-input {
  width: 100%;
  padding: 12px;
  border: 1px solid #ddd;
  border-radius: 8px;
  font-size: 14px;
  transition:
    border-color 0.2s,
    box-shadow 0.2s;
}

.form-input:focus {
  outline: none;
  border-color: #007bff;
  box-shadow: 0 0 0 2px rgba(0, 123, 255, 0.25);
}

.form-input::placeholder {
  color: #999;
}

.input-group {
  display: flex;
  gap: 8px;
}

.form-select-small {
  padding: 12px;
  border: 1px solid #ddd;
  border-radius: 8px;
  font-size: 14px;
  background: white;
  min-width: 70px;
}

.form-select-small:focus {
  outline: none;
  border-color: #007bff;
  box-shadow: 0 0 0 2px rgba(0, 123, 255, 0.25);
}

.form-input-flex {
  flex: 1;
  padding: 12px;
  border: 1px solid #ddd;
  border-radius: 8px;
  font-size: 14px;
}

.form-input-flex:focus {
  outline: none;
  border-color: #007bff;
  box-shadow: 0 0 0 2px rgba(0, 123, 255, 0.25);
}

.form-input-flex::placeholder {
  color: #999;
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
  margin-bottom: 16px;
}

.submit-btn:hover {
  background: #0056b3;
}

.login-link {
  text-align: center;
  font-size: 14px;
  color: #666;
}

.login-link span {
  margin-right: 4px;
}

.link-button {
  background: none;
  border: none;
  color: #007bff;
  cursor: pointer;
  text-decoration: underline;
  font-size: 14px;
}

.link-button:hover {
  color: #0056b3;
}
</style>
