<script>
  export default {
    data() {
      return {
        nuevaTarea: {
          titulo: '',
          descripcion: '',
          fecha: '',
          prioridad: 'Alta',
          editarTarea: null,
        },
        mensaje: '',
        camposIncompletos: false,
      };
    },
    methods: {
      agregarTarea() {
        if (this.nuevaTarea.titulo === '' || this.nuevaTarea.fecha === '') {
          this.camposIncompletos = true;
          this.mensaje = 'Hay campos sin rellenar';
        } else {
          this.$emit('nueva-tarea', this.nuevaTarea);
          this.nuevaTarea = {
            titulo: '',
            descripcion: '',
            fecha: '',
            prioridad: 'alta',
            etiqueta: '',
          };
          this.mensaje = 'Tarea agregada';
          this.camposIncompletos = false;
        }
      },
      getFechaActual() {
        const hoy = new Date();
        const yyyy = hoy.getFullYear();
        const mm = String(hoy.getMonth() + 1).padStart(2, '0');
        const dd = String(hoy.getDate()).padStart(2, '0');
        return `${yyyy}-${mm}-${dd}`;
      },
    },
  };
</script>

<template>
  <nav>
    <form @submit.prevent="agregarTarea">
      <h1>Formulario </h1>
      <p>Título de la tarea: </p>
      <input type="text" v-model="nuevaTarea.titulo">

      <label>Descripción de la tarea: </label>
      <textarea v-model="nuevaTarea.descripcion"></textarea>

      <label>Fecha de vencimiento: </label>
      <input type="date" v-model="nuevaTarea.fecha" :min="getFechaActual()" />

      <label>Prioridad: </label>
      <select id="prioridad" v-model="nuevaTarea.prioridad">
        <option value="Alta">Alta</option>
        <option value="Media">Media</option>
        <option value="Baja">Baja</option>
      </select>

      <label>Etiqueta: </label>
      <input type="text" v-model="nuevaTarea.etiqueta"/>
      <p v-if="camposIncompletos" class="mensaje-error">{{ mensaje }}</p>
      <p v-if="mensaje === 'Tarea agregada'" class="mensaje-exito">{{ mensaje }}</p>
      <button type="submit">Subir</button>
    </form>
  </nav>
</template>

<style scoped>
  nav {
    height: 100%;
  }

  form {
    display: flex;
    align-items: flex-start;
    justify-content: center;
    flex-direction: column;
    gap: 5px;
    background-color: rgb(53, 53, 53);
    padding: 10px;
    border-radius: 5px;
  }

  label, button {
    margin-top: 10px;
  }

  input, textarea, select, button {
    width: 100%;
    border: none;
    background-color: #5f5f5f;
    color: white;
    border-radius: 5px;
    padding: 10px;
  }

  textarea {
    resize: vertical;
  }

  button {
    cursor: pointer;
    background-color: #181818;
  }
</style>
