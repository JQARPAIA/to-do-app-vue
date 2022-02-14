<template>
  <div class="m-0 p-0">
    <div 
      class="alert d-flex justify-content-between align-items-center mt-3"
      :class="{
        'alert-warning': !tarea.isCompleted,
        'alert-success': tarea.isCompleted,
      }"
      role="alert" 
    >
      <p class="m-0" :class="{'isCompleted': tarea.isCompleted}">{{ tarea.tarea }}</p>
      <div>
        <button
          type="button" 
          class="btn btn-labeled btn-success me-1"
          @click="taskDone(tarea.id)"
        >
          <i v-if="tarea.isCompleted" class="fa-solid fa-undo-alt text-white  "></i>
          <i v-if="!tarea.isCompleted" class="fa-solid fa-circle-check text-white"></i>
        </button>
        <button 
          type="button" 
          class="btn btn-labeled btn-danger"
          data-bs-toggle="modal"
          data-bs-target="#myModal"
        >
          <i class="fa fa-trash"></i>
        </button>   
      </div>
    </div>

    <!-- The Modal -->
    <div class="modal" id="myModal">
      <div class="modal-dialog modal-dialog-centered">
        <div class="modal-content">

          <!-- Modal Header -->
          <div class="modal-header">
            <h4 class="modal-title">¿Estás seguro?</h4>
          </div>

          <!-- Modal body -->
          <div class="modal-body">
            Esta acción es irreversible.
          </div>

          <!-- Modal footer -->
          <div class="modal-footer">
            <button type="button" class="btn btn-success" data-bs-dismiss="modal">Cancelar</button>
            <button type="button" class="btn btn-danger" @click="deleteTask(tarea.id)" data-bs-dismiss="modal">Borrar</button>
          </div>

        </div>
      </div>
    </div>

  </div>
</template>
<script>
import { inject } from '@vue/runtime-core'
export default {
  props: {
    tarea: {
      type: Object,
      required: true,
      default: {}
    }
  },
  setup() {
    const tareas = inject('tareas')

    const taskDone = (id) => {
      tareas.value = tareas.value.map(item => {
        if(item.id === id) {
          item.isCompleted = !item.isCompleted
        }
        return item
      })
    }
    const deleteTask = (id) => {
      tareas.value = tareas.value.filter(item => {
        return item.id !== id
      })
    }

    return { tareas, taskDone, deleteTask }
  }
  
}
</script>
<style scoped>
  .isCompleted {
    text-decoration: line-through;
  }
  #myModal {
    color: black;
  }
</style>