<template>
  <div class="menu-container">
    <div class="menu-card">
      <div class="logo-container">
        <img
          src=""
          alt="A&S Logo"
          class="logo-as"
        />
        <img
          src=""
          alt="UPB Logo"
          class="logo-upb"
        />
      </div>
      <h1 class="menu-title">Menu</h1>

      <div class="menu-buttons">
        <button class="menu-btn" @click="$emit('changeView', 'form')">
          <span class="icon">✔️</span>
          Registrar limpieza <span class="arrow">></span>
        </button>

        <button
          @click="$emit('changeView', 'historial')"
          class="menu-btn"
        >
          📄 Ver historial
        </button>

        <button
          @click="$emit('changeView', 'login')"
          class="menu-btn"
        >
          🚪 Cerrar sesión
        </button>

      </div>
    </div>
  </div>
</template>

<script setup>
const emit = defineEmits(['changeView'])
</script>

<style scoped>
.menu-container {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  background-color: #f0f4f7;
  padding: 20px;
  font-family: Arial, sans-serif;
}

.menu-card {
  width: 100%;
  max-width: 400px;
  background-color: #ffffff;
  border-radius: 12px;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
  padding: 30px;
  box-sizing: border-box;
}

.logo-container {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 20px;
  margin-bottom: 30px;
}

.logo-as {
  width: 70px;
  height: auto;
}

.logo-upb {
  width: 70px;
  height: auto;
}

.menu-title {
  font-size: 28px;
  font-weight: bold;
  color: #333333;
  margin-bottom: 30px;
}

.menu-buttons {
  display: flex;
  flex-direction: column;
  gap: 15px;
}

.menu-btn {
  width: 100%;
  padding: 16px 24px;
  background-color: #007bff;
  color: #ffffff;
  border: none;
  border-radius: 8px;
  font-size: 16px;
  font-weight: 500;
  cursor: pointer;
  transition: background-color 0.2s ease;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.menu-btn:hover {
  background-color: #0056b3;
}

.icon {
  font-size: 18px;
  margin-right: 12px;
}

.arrow {
  font-weight: bold;
}
</style>