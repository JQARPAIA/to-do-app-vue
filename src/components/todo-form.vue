<template>
  <form @submit.prevent="addTask">
    <input
      type="text"
      class="form-control my-3"
      placeholder="Agregue una tarea"
      v-model.trim="tarea"
    />
    <button class="btn btn-primary w-100">Agregar tarea</button>
  </form>
</template>
<script>
import { inject, ref } from '@vue/runtime-core'
export default {
  setup(){
    const tareas = inject('tareas')
    const tarea = ref('')

    const addTask = () => {
      if (tarea.value === '') {
        return
      }

      const tareaToAdd = {
        tarea: tarea.value,
        isCompleted: false,
        id: Date.now()
      }
      
      tareas.value.push(tareaToAdd)
      tarea.value = ''
    }
    return { tarea, addTask }
  }
}
</script>
<style lang="">
  
</style>