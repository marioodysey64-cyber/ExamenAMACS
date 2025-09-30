<template>
  <div class="cuestionario">
    <h1>Cuestionario Básico</h1>

    <div v-if="current < preguntas.length">
      <h2>{{ preguntas[current].texto }}</h2>
      <ul>
        <li v-for="(opcion, index) in preguntas[current].opciones" :key="index">
          <button @click="responder(index)">
            {{ opcion }}
          </button>
        </li>
      </ul>
    </div>

    <div v-else>
      <h2>¡Cuestionario completado!</h2>
      <p>Tu puntuación: {{ puntuacion }} de {{ preguntas.length }}</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      current: 0,
      puntuacion: 0,
      preguntas: [
        {
          texto: '¿Cuál es la capital de El Salvador?',
          opciones: ['San Miguel', 'Santa Ana', 'San Salvador', 'La Libertad'],
          correcta: 2
        },
        {
          texto: '¿Cuánto es 5 × 6?',
          opciones: ['30', '11', '56', '25'],
          correcta: 0
        },
        {
          texto: '¿Qué lenguaje se usa en Vue?',
          opciones: ['Python', 'JavaScript', 'C++', 'Ruby'],
          correcta: 1
        }
      ]
    }
  },
  methods: {
    responder(indice) {
      if (indice === this.preguntas[this.current].correcta) {
        this.puntuacion++
      }
      this.current++
    }
  }
}
</script>

<style scoped>
.cuestionario {
  max-width: 600px;
  margin: auto;
  padding: 2rem;
  font-family: Arial, sans-serif;
}
button {
  display: block;
  margin: 0.5rem 0;
  padding: 0.75rem;
  width: 100%;
  background-color: #0078d4;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}
button:hover {
  background-color: #005a9e;
}
</style>