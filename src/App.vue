<script setup>
  import { ref } from 'vue';
  import Header from './components/Header.vue';
  import Homework from './components/Homework.vue';
  import Navbar from './components/Navbar.vue';

  const tareas = ref([]);

  const agregarTarea = (nuevaTarea) => {
    tareas.value.push(nuevaTarea);
  };
</script>

<template>
  <div class="app">
    <div class="header">
      <Header />
    </div>
    <div class="main">
      <div class="main-content">
        <Navbar class="nav" @nueva-tarea="agregarTarea" />
        <div class="content">
          <Homework :tareas="tareas" />
        </div>
      </div>
    </div>
  </div>
</template>

<style>
  .app {
    display: flex;
    flex-direction: column;
    height: 100vh;
    color: white;
  }

  .main {
    width: 100%;
    margin: 0px 10px;
  }

  .main-content {
    position: absolute;
    display: flex;
    flex: 1; 
    width: calc(100% - 20px);
    gap: 10px;
}

  .nav {
    width: 25%; 
  }

  .content {
    flex: 1;
  }

  
  @media (max-width: 1024px) {
    .header {
      position: relative;
    }
    .main-content {
      position: relative;
      display: flex;
      flex-direction: column;
    }

    .nav {
      width: 100%; 
    }

    .content {
      flex: 1;
    }
  }
</style>
