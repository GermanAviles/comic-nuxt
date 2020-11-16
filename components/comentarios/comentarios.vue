<template>
  <div class="comentarios">
    <div v-for="(comentario, i) of comentarios" :key="i+1" class="comentario">
      <div class="header-comentario">
        <span class="titulo"> {{ comentario.titulo }} </span>
        <span class="calificacion"> {{ comentario.calificacion }} / 5</span>
      </div>
      <div class="body-comentario">
        {{ comentario.descripcion }}
      </div>
    </div>
    <div v-if="!comentarios.length" class="sin-comentarios" >
      SIN COMENTARIOS
    </div>
  </div>
</template>

<script>
export default {
  auth: false,
  layout: 'baseLayout',
  components: {
  },
  mixins: [],
  props: {
    comentarios: {
      type: null,
      required: true,
      default: []
    }
  },
  data: () => ({}),

  computed: {
  },

  watch: { },

  mounted() {
  },

  created() {
  },

  methods: {
  },
  beforeDestroy() {
  }
}
</script>

<style>
.sin-comentarios {
  height: 100%;
  display: flex;
  flex-flow: row wrap;
  justify-content: center;
  align-items: center;
  font-size: 2rem;
  font-weight: bold;
  color: rgba(0, 0, 0, 0.329);
}

.comentarios {
  padding: 10px;
  max-height: 100%;
}
.comentarios .comentario {
  border: 1px solid #00000036;
  border-radius: 4px;
  padding: 10px;
  max-height: 20vh;
  height: auto;
  margin-bottom: 15px;
}
.comentarios .comentario .header-comentario {
  margin-bottom: 10px;
  padding: 5px 0;
  border-bottom: 1px dashed #9c9393;
}
</style>
