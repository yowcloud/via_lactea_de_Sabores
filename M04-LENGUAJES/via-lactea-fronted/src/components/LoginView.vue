<template>
    <video autoplay muted loop class="video-background">
      <source src="../assets/video/space_back.mp4" type="video/mp4">
      Tu navegador no soporta el elemento de video.
    </video>
    <div class="login-container">
      <div class="login-box">
        <h2>Login</h2>
        <form @submit.prevent="login" class="login-form">
          <div class="form-group">
            <label for="email">Email:</label>
            <input type="email" id="email" v-model="email" required>
          </div>
          <div class="form-group">
            <label for="contrasena">Contraseña:</label>
            <input type="password" id="contrasena" v-model="contrasena" required>
          </div>
          <button type="submit" class="login-button">Iniciar sesión</button>
          <div class="text-center">
            <p>¿No tienes una cuenta? <router-link to="/registro">Registrarse</router-link></p>
          </div>
        </form>
      </div>
    </div>
</template>

<script>
export default {
  data() {
    return {
      email: '',
      contrasena: ''
    };
  },
  methods: {
    async login() {
      try {
        const response = await fetch('http://localhost:8081/api/login', {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json'
          },
          body: JSON.stringify({
            email: this.email,
            contrasena: this.contrasena
          })
        });

        if (response.ok) {
          // Inicio de sesión exitoso, redirigir a otra página
          alert('Inicio de sesión correcto! ENTRANDO');
          this.$router.push('/home');
        } else {
          // Error en el inicio de sesión, mostrar mensaje de error
          console.error('Error en el inicio de sesión:', response.statusText);
          alert('Inicio de sesión fallido. Por favor, verifica tus credenciales.');
        }
      } catch (error) {
        // Error en la solicitud HTTP
        console.error('Error en la solicitud HTTP:', error);
        alert('Ha ocurrido un error. Por favor, inténtalo de nuevo más tarde.');
        //this.$router.push('/home');

      }
    }
  }
};
</script>

<style scoped>
@import "../assets/css/login.css";
/* Estilos específicos del componente Login */
</style>
