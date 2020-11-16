<template>
  <div class="container">
    <div v-if="!comic" class="loading">
      <loading />
    </div>
    <div v-if="comic" class="cont-comic">
      <div class="comic">
        <card
          :srcImage="comic.img"
          :titulo="comic.title"
          :descripcion="comic.transcript"
          @refreshComic="cargarComic()"
          @crearComentario="nuevoCometario($event)"
        />
      </div>
      <div class="comentarios-comic">
        <comentarios :comentarios="comentarios" />
      </div>
    </div>
  </div>
</template>

<script>
import card from '../components/card/card'
import loading from '../components/loading/loading'
import comentarios from '../components/comentarios/comentarios'

export default {
  auth: false,
  layout: 'baseLayout',
  components: {
    card,
    loading,
    comentarios
  },
  mixins: [],
  props: {
  },
  data: () => ({
    comic: null,
    comentarios: []
  }),

  computed: {
  },

  watch: { },

  mounted() {
    this.cargarComic()
  },

  created() {
  },

  methods: {
    cargarComic() {
      this.comic = null;
      const idComic = Math.floor(Math.random() * 1000);
      this.$axios.$get(`comic/${idComic}` ).then((response) => {
        this.comic = response.data
      })
    },

    nuevoCometario( comentario ) {
      this.comentarios.push(comentario);
    }
  },
  beforeDestroy() {
  }
}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}

.cont-comic{
  display: grid;
  grid-template-columns: 2fr 1fr;
  grid-gap: 20px;
}

.comentarios-comic{
  overflow-y: auto;
  height: 83vh;
}

.comic {
  width: 100%;
  height: 100%;
}
</style>
