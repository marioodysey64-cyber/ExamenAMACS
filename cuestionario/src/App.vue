<template>
  <form class="cuestionario" @submit.prevent="calcularPuntuacion">
    <h1>Formulario de Cuestionario</h1>

    <div v-for="(pregunta, index) in preguntas" :key="index" class="pregunta">
      <h2>{{ pregunta.texto }}</h2>
      <div v-for="(opcion, i) in pregunta.opciones" :key="i">
        <label>
          <input
            type="radio"
            :name="'pregunta-' + index"
            :value="i"
            v-model.number="respuestas[index]"
            required
          />
          {{ opcion }}
        </label>
      </div>
    </div>

    <button type="submit">Enviar respuestas</button>

    <div v-if="mostrarResultado" class="resultado">
      <h2>Resultado</h2>
      <p>Tu puntuación: {{ puntuacion }} de {{ preguntas.length }}</p>
    </div>
  </form>
</template>

<script>
export default {
  data() {
    return {
      preguntas: [
        {
          texto: '¿Cuál es la capital de El Salvador?',
          opciones: ['Santa Ana', 'San Salvador', 'La Libertad', 'San Miguel'],
          correcta: 1
        },
        {
          texto: '¿Qué significa HTML?',
          opciones: [
            'HyperText Markup Language',
            'HighText Machine Language',
            'HyperTool Multi Language',
            'None of the above'
          ],
          correcta: 0
        },
        {
          texto: '¿Qué framework usa Vue?',
          opciones: ['React', 'Angular', 'JavaScript', 'Vue.js'],
          correcta: 3
        }
      ],
      respuestas: Array(3).fill(null),
      puntuacion: 0,
      mostrarResultado: false
    }
  },
  methods: {
    calcularPuntuacion() {
      this.puntuacion = this.respuestas.reduce((total, respuesta, index) => {
        return respuesta === this.preguntas[index].correcta ? total + 1 : total
      }, 0)
      this.mostrarResultado = true
    }
  }
}
</script>

<style scoped>
.cuestionario {
  max-width: 600px;
  margin: auto;
  padding: 2rem;
  font-family: 'Segoe UI', sans-serif;
}
.pregunta {
  margin-bottom: 2rem;
}
label {
  display: block;
  margin: 0.5rem 0;
}
button {
  padding: 0.75rem 1.5rem;
  background-color: #0078d4;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}
button:hover {
  background-color: #005a9e;
}
.resultado {
  margin-top: 2rem;
  background: #f0f8ff;
  padding: 1rem;
  border-radius: 6px;
}
</style>