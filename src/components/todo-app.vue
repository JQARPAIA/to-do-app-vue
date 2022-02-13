<template>
  <h1>
    To-Do App
  </h1>
  <todo-form />
  <tarea 
    v-for="(tarea, index) in tareas" :key="index"
    :tarea="tarea"
  />

  <div 
    v-if="tareas.length === 0"
    class="alert alert-primary d-flex justify-content-between align-items-center mt-3"
  >
    No hay pendientes.
  </div>
</template>
<script>
import TodoForm from '@/components/todo-form.vue'
import { ref } from '@vue/reactivity'
import { provide, watchEffect } from '@vue/runtime-core'
import Tarea from './tarea.vue'
export default {
  components: {
    TodoForm,
    Tarea
  },
  setup() {
    const tareas = ref([])
    provide('tareas', tareas)

    if (localStorage.getItem('tareasToDoApp')) {
      tareas.value = JSON.parse(localStorage.getItem('tareasToDoApp'))
    }

    watchEffect(() => {
      localStorage.setItem('tareasToDoApp', JSON.stringify(tareas.value))
      console.log(tareas.value.length)
    })

    return { tareas }
  }
}
</script>