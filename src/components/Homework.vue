<script setup>
  import { ref, defineProps, defineEmits, computed } from 'vue';
  
  const props = defineProps({
    tareas: Array,
  });

  const { emit } = defineEmits();

  const eliminarTarea = (index) => {
    if (index >= 0 && index < props.tareas.length) {
      props.tareas.splice(index, 1);
    }
  };

  const formatearFecha = (fecha) => {
    const options = { year: 'numeric', month: 'numeric', day: 'numeric' };
    return new Date(fecha).toLocaleDateString(undefined, options);
  };

  const tareasOrdenadas = computed(() => {
    return [...props.tareas].sort((a, b) => {
      return new Date(a.fecha) - new Date(b.fecha);
    });
  });
</script>

<template>
  <section>
    <div>
      <h1>Tareas</h1>
    </div>
    <div class="homeworks-content">
      <div v-if="tareasOrdenadas.length === 0">
        <p>No hay tareas que mostrar.</p>
      </div>
      <div v-else class="homeworks">
        <div v-for="(tarea, index) in tareasOrdenadas" :key="index" class="homework">
          <div class="encabezado-tarea">
            <h2>{{ tarea.titulo }}</h2>
            <p>{{ formatearFecha(tarea.fecha) }}</p>
          </div>
          <div class="contenido-tarea">
            <h4>Prioridad: {{ tarea.prioridad }}</h4>
            <h4>Etiqueta: {{ tarea.etiqueta }} </h4>
            <p>{{ tarea.descripcion }}</p>
            <div class="buttons">
              <button @click="eliminarTarea(index)">Eliminar</button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
  section {
    background-color: rgb(53, 53, 53);
    display: flex;
    align-items: flex-start;
    justify-content: center;
    flex-direction: column;
    padding: 10px;
    border-radius: 5px;
    width: 100%;
  }
  .homeworks-content {
    width: 100%;
  }

  .homeworks {
    margin-top: 10px;
    display: flex;
    flex-direction: column;
    gap: 10px;
    width: 100%;
  }

  .homework {
    width: 100%;
  }

  .encabezado-tarea {
    padding: 10px;
    background-color: #181818;
    border-radius: 5px 5px 0px 0px;
    display: flex;
    align-items: center;
    justify-content: space-between;
  }

  .contenido-tarea {
    padding: 10px;
    background-color: #474747;
    border-radius: 0px 0px 5px 5px;
  }

  h4 {
    font-weight: 700;
  }

  .buttons {
    display: flex;
    margin-top: 10px;
    gap: 10px;
  }

  button {
    width: 80px;
    border: none;
    border-radius: 5px;
    padding: 10px;
    border: none;
    color: white;
    cursor: pointer;
    background-color: #181818;
  }
</style>