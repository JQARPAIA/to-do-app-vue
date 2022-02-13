<template>
  <div class="d-flex flex-column justify-content-between vh-100">
    <div class="container mt-3">
      <todo-app/>
    </div>
    <div class="h5 d-flex justify-content-center align-items-center">
      <p>Creado por <a href="https://josearpaiaq.netlify.app/" class="fw-bold text-decoration-none"  target="blank">Jose Arpaia</a></p>
    </div>
  </div>
</template>

<script>
import TodoApp from './components/todo-app.vue'

export default {
  name: 'App',
  components: {TodoApp}
}
</script>
