<script setup>
import { ref, computed } from 'vue'

const busqueda = ref('')
const generoActivo = ref('')

const peliculas = ref([
  { id: 1, nombre: 'Avengers: Endgame', genero: 'accion', rating: 10 },
  { id: 2, nombre: 'The Dark Knight', genero: 'accion', rating: 10 },
  { id: 3, nombre: 'Gladiator', genero: 'accion', rating: 9 },
  { id: 4, nombre: 'Mad Max: Fury Road', genero: 'accion', rating: 9 },
  { id: 5, nombre: 'John Wick', genero: 'accion', rating: 9 },
  { id: 6, nombre: 'Die Hard', genero: 'accion', rating: 8 },
  { id: 7, nombre: 'The Matrix', genero: 'accion', rating: 10 },
  { id: 8, nombre: 'Black Panther', genero: 'accion', rating: 8 },
  { id: 9, nombre: 'Iron Man', genero: 'accion', rating: 9 },
  { id: 10, nombre: 'Mission Impossible', genero: 'accion', rating: 8 },

  { id: 11, nombre: 'The Hangover', genero: 'comedia', rating: 9 },
  { id: 12, nombre: 'Superbad', genero: 'comedia', rating: 8 },
  { id: 13, nombre: 'Step Brothers', genero: 'comedia', rating: 8 },
  { id: 14, nombre: 'Ted', genero: 'comedia', rating: 7 },
  { id: 15, nombre: 'Grown Ups', genero: 'comedia', rating: 7 },
  { id: 16, nombre: 'White Chicks', genero: 'comedia', rating: 8 },
  { id: 17, nombre: 'The Mask', genero: 'comedia', rating: 9 },
  { id: 18, nombre: 'Dumb and Dumber', genero: 'comedia', rating: 8 },
  { id: 19, nombre: '21 Jump Street', genero: 'comedia', rating: 8 },
  { id: 20, nombre: 'Mean Girls', genero: 'comedia', rating: 8 },

  { id: 21, nombre: 'The Conjuring', genero: 'terror', rating: 9 },
  { id: 22, nombre: 'Insidious', genero: 'terror', rating: 8 },
  { id: 23, nombre: 'It', genero: 'terror', rating: 8 },
  { id: 24, nombre: 'Annabelle', genero: 'terror', rating: 7 },
  { id: 25, nombre: 'Hereditary', genero: 'terror', rating: 9 },
  { id: 26, nombre: 'The Exorcist', genero: 'terror', rating: 10 },
  { id: 27, nombre: 'A Quiet Place', genero: 'terror', rating: 8 },
  { id: 28, nombre: 'Sinister', genero: 'terror', rating: 8 },
  { id: 29, nombre: 'The Nun', genero: 'terror', rating: 7 },
  { id: 30, nombre: 'Saw', genero: 'terror', rating: 8 },

  { id: 31, nombre: 'Titanic', genero: 'romance', rating: 10 },
  { id: 32, nombre: 'The Notebook', genero: 'romance', rating: 9 },
  { id: 33, nombre: 'La La Land', genero: 'romance', rating: 9 },
  { id: 34, nombre: 'Me Before You', genero: 'romance', rating: 8 },
  { id: 35, nombre: 'Pride & Prejudice', genero: 'romance', rating: 9 },
  { id: 36, nombre: 'Romeo + Juliet', genero: 'romance', rating: 8 },
  { id: 37, nombre: 'Love Actually', genero: 'romance', rating: 9 },
  { id: 38, nombre: 'Notting Hill', genero: 'romance', rating: 8 },
  { id: 39, nombre: 'The Fault in Our Stars', genero: 'romance', rating: 8 },
  { id: 40, nombre: 'Before Sunrise', genero: 'romance', rating: 9 },

  { id: 41, nombre: 'Interstellar', genero: 'ciencia', rating: 10 },
  { id: 42, nombre: 'Inception', genero: 'ciencia', rating: 10 },
  { id: 43, nombre: 'The Matrix', genero: 'ciencia', rating: 10 },
  { id: 44, nombre: 'Blade Runner 2049', genero: 'ciencia', rating: 9 },
  { id: 45, nombre: 'Arrival', genero: 'ciencia', rating: 9 },
  { id: 46, nombre: 'Gravity', genero: 'ciencia', rating: 8 },
  { id: 47, nombre: 'Dune', genero: 'ciencia', rating: 9 },
  { id: 48, nombre: 'Avatar', genero: 'ciencia', rating: 9 },
  { id: 49, nombre: 'Star Wars', genero: 'ciencia', rating: 10 },
  { id: 50, nombre: 'E.T.', genero: 'ciencia', rating: 9 }
])

const peliculasFiltradas = computed(() => {
  return peliculas.value
    .filter(p => {
      const coincideNombre = p.nombre.toLowerCase().includes(busqueda.value.toLowerCase())
      const coincideGenero = generoActivo.value === '' || p.genero === generoActivo.value
      return coincideNombre && coincideGenero
    })
    .sort((a, b) => b.rating - a.rating)
})

const filtrarGenero = (genero) => {
  generoActivo.value = genero
}
</script>

<template>
  <div class="container">
    <h1>🎬 Catálogo de Películas</h1>

    <input v-model="busqueda" placeholder="Buscar en tiempo real...">

    <div class="botones">
      <button @click="filtrarGenero('accion')">Acción</button>
      <button @click="filtrarGenero('comedia')">Comedia</button>
      <button @click="filtrarGenero('terror')">Terror</button>
      <button @click="filtrarGenero('romance')">Romance</button>
      <button @click="filtrarGenero('ciencia')">Ciencia</button>
      <button @click="filtrarGenero('')">Todos</button>
    </div>

    <!-- 🔥 CONTENEDOR SCROLL -->
    <div class="tabla-scroll">
      <table v-if="peliculasFiltradas.length > 0">
        <thead>
          <tr>
            <th>Película</th>
            <th>Género</th>
            <th>⭐</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="p in peliculasFiltradas" :key="p.id">
            <td>{{ p.nombre }}</td>
            <td>{{ p.genero }}</td>
            <td>{{ p.rating }}</td>
          </tr>
        </tbody>
      </table>

      <p v-else>No hay resultados 😢</p>
    </div>
  </div>
</template>

<style>
body {
  background: #111;
  font-family: Arial;
}

/* 📦 CAJA GRANDE Y FIJA */
.container {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);

  width: 900px;
  height: 600px;

  padding: 20px;
  border-radius: 10px;
  text-align: center;

  background: linear-gradient(rgba(0,0,0,0.7), rgba(0,0,0,0.7)),
  url('https://png.pngtree.com/thumb_back/fh260/background/20250307/pngtree-a-vibrant-movie-themed-background-with-the-film-reels-camera-and-image_17080149.jpg');

  background-size: cover;
  color: white;

  box-shadow: 0 0 20px rgba(0,0,0,0.8);
}

/* 🔥 SCROLL SOLO AQUÍ */
.tabla-scroll {
  margin-top: 10px;
  height: 350px;
  overflow-y: auto;
}

/* INPUT */
input {
  width: 100%;
  padding: 8px;
}

/* BOTONES */
button {
  margin: 5px;
  padding: 8px;
  border: none;
  cursor: pointer;
  background: black;
  color: white;
}

/* TABLA */
table {
  width: 100%;
  border-collapse: collapse;
  background: rgba(255,255,255,0.9);
  color: black;
}

th, td {
  border: 1px solid #ccc;
  padding: 8px;
}

th {
  background: black;
  color: white;
}
</style>