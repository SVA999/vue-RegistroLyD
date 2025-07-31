<template>
  <div class="main-container">
    <div class="login-card">
      <div class="header">
      <div class="logo">UPB</div>
      <h1 class="title">Inicio de sesión</h1>
    </div>
      

      <form @submit.prevent="handleLogin">
        <div class="form-group">
          <label class="form-label">Documento de identidad</label>
          <div class="input-group">
            <select v-model="formData.docType" class="input-select">
              <option value="CC">CC</option>
              <option value="TI">TI</option>
              <option value="CE">CE</option>
            </select>
            <input
              type="text"
              v-model="formData.docNumber"
              placeholder="1011515455"
              class="input-field"
              required
            />
          </div>
        </div>

        <div class="form-group">
          <label class="form-label">Contraseña</label>
          <input
            type="password"
            v-model="formData.password"
            placeholder="••••••••••••"
            class="input-field"
            required
          />
          <div v-if="loginSuccess" class="success-message">
            <span class="success-icon">✓</span> ¡Bienvenid@!!
          </div>
        </div>

        <button type="submit" class="submit-btn">
          Iniciar
          <span class="arrow-icon">></span>
        </button>

        <div class="form-group readonly-field">
          <label class="form-label">Sector</label>
          <div class="input-readonly">
            <span class="icon">🎓</span>
            <input type="text" value="Educativo" readonly class="input-field" />
          </div>
        </div>

        <div class="form-group readonly-field">
          <label class="form-label">Locacion</label>
          <div class="input-readonly">
            <span class="icon">📍</span>
            <input
              type="text"
              value="Universidad Pontificia Bolivariana"
              readonly
              class="input-field"
            />
          </div>
        </div>

        <div class="form-group readonly-field">
          <label class="form-label">Area</label>
          <div class="input-readonly">
            <span class="icon">🛡️</span>
            <input type="text" value="Limpieza" readonly class="input-field" />
          </div>
        </div>
      </form>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const formData = ref({
  docType: 'CC',
  docNumber: '',
  password: '',
})

const loginSuccess = ref(false)
const emit = defineEmits(['changeView'])

function handleLogin() {
  // Aquí se manejaría la lógica de autenticación real
  // Por ahora, simulamos un inicio de sesión exitoso
  loginSuccess.value = true

  // Opcional: emitir un evento para cambiar la vista después de un tiempo
  setTimeout(() => {
    emit('changeView', 'menu')
  }, 1500)
}
</script>

<style scoped>
.main-container {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  background-color: #f0f4f7;
  padding: 20px;
  font-family: Arial, sans-serif;
}

.login-card {
  width: 100%;
  max-width: 400px;
  background-color: #ffffff;
  border-radius: 12px;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
  padding: 30px;
  box-sizing: border-box;
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

.logo-container {
  text-align: center;
  margin-bottom: 20px;
}

.logo-img {
  width: 100px;
  height: auto;
}

.title {
  text-align: center;
  font-size: 28px;
  font-weight: bold;
  color: #333333;
  margin-bottom: 30px;
}

.form-group {
  margin-bottom: 20px;
}

.form-label {
  display: block;
  font-size: 14px;
  font-weight: bold;
  color: #555555;
  margin-bottom: 8px;
}

.input-group {
  display: flex;
  border: 1px solid #e0e0e0;
  border-radius: 8px;
  overflow: hidden;
  background-color: #f9f9f9;
}

.input-select {
  padding: 12px 10px;
  border: none;
  background-color: #e9ecef;
  color: #555555;
  font-weight: 600;
  border-right: 1px solid #e0e0e0;
  cursor: pointer;
  -webkit-appearance: none;
  -moz-appearance: none;
  appearance: none;
  background-image: url("data:image/svg+xml,%3csvg xmlns='http://www.w3.org/2000/svg' fill='none' viewBox='0 0 20 20'%3e%3cpath stroke='%236b7280' stroke-linecap='round' stroke-linejoin='round' stroke-width='1.5' d='M6 8l4 4 4-4'/%3e%3c/svg%3e");
  background-repeat: no-repeat;
  background-position: right 8px center;
  background-size: 16px;
  padding-right: 25px;
}

.input-field {
  flex-grow: 1;
  padding: 12px;
  border: none;
  background-color: #f9f9f9;
  font-size: 16px;
  color: #333333;
  outline: none;
}

.input-field::placeholder {
  color: #aaaaaa;
}

.input-field:focus {
  background-color: #ffffff;
}

/* Estilos para el campo de contraseña */
input[type='password'] {
  width: 100%;
  padding: 12px;
  border: 1px solid #e0e0e0;
  border-radius: 8px;
  background-color: #f9f9f9;
  box-sizing: border-box;
}

.success-message {
  color: #28a745;
  font-size: 14px;
  font-weight: bold;
  margin-top: 8px;
  display: flex;
  align-items: center;
}

.success-icon {
  font-size: 18px;
  margin-right: 5px;
  color: #28a745;
}

.submit-btn {
  width: 100%;
  padding: 14px;
  background-color: #007bff;
  color: #ffffff;
  border: none;
  border-radius: 8px;
  font-size: 16px;
  font-weight: bold;
  cursor: pointer;
  transition: background-color 0.2s ease;
  margin-top: 10px;
  display: flex;
  justify-content: center;
  align-items: center;
}

.submit-btn:hover {
  background-color: #0056b3;
}

.arrow-icon {
  margin-left: 8px;
}

.readonly-field {
  margin-top: 25px;
}

.input-readonly {
  display: flex;
  align-items: center;
  padding: 10px 12px;
  border: 1px solid #e0e0e0;
  border-radius: 8px;
  background-color: #f9f9f9;
}

.input-readonly .icon {
  font-size: 18px;
  color: #888888;
  margin-right: 10px;
}

.input-readonly .input-field {
  background-color: transparent;
  padding: 0;
  border: none;
  color: #555555;
  font-size: 16px;
}
</style>