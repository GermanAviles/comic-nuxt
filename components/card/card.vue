<template>
  <div class="card-comic">
    <!-- Imagen del comic -->
    <div class="cont-img-comic">
      <img id="comic-image" :src="srcImage" alt="imagen-comic" >
    </div>
    <!-- Información comic -->
    <div id="cont-info-comic" class="cont-info-comic">
      <!-- titulo del comic -->
      <div class="cont-title">
        <h1 id="titulo-comic"> {{ titulo }} </h1>
        <span id="icono-refresh" class="icono-refresh material-icons" @click="refrescar()">cached</span>
      </div>
      <!-- Descripción -->
      <div class="descripcion-comic">
        <p id="descripcion-comic"> {{ descripcion }} </p>
      </div>
      <!-- Calificación del comic -->
      <rating-stars @rating="agregarCalificacion($event)" />
      <!-- Comentario -->
      <div class="cont-comentario">
        <textarea v-model="descripcionComentario" name="comentario" id="comentario-comic" cols="30" rows="10" />
      </div>
      <div class="cont-botones">
        <a href="javascript:void(0);" class="btn btn-danger" @click="limpiarInputs()"> Cancelar </a>
        <a href="javascript:void(0);" class="btn btn-succes" @click="agregarComentario()"> Guardar </a>
      </div>
    </div>
</div>
</template>

<script>
import ratingStars from '../rating-stars/rating-stars'
export default {
  auth: false,
  layout: 'baseLayout',
  components: {
    'rating-stars': ratingStars
  },
  mixins: [],
  props: {
    srcImage: {
      type: String,
      required: true,
      default: ''
    },
    titulo: {
      type: String,
      required: true,
      default: ''
    },
    descripcion: {
      type: String,
      required: true,
      default: ''
    }
  },
  data: () => ({
    descripcionComentario: null,
    calificacionComic: 0
  }),

  computed: {
  },

  watch: { },

  mounted() {
  },

  created() {
  },

  methods: {
    agregarCalificacion( value ) {
      this.calificacionComic = value
    },

    refrescar() {
      this.$emit('refreshComic', true)
    },

    limpiarInputs() {
      this.descripcionComentario = null
      this.calificacionComic = 0
      this.$root.$emit('reiniciarnputs', true)
    },

    agregarComentario() {
      const comentario = {
        titulo: this.titulo,
        descripcion: this.descripcionComentario,
        calificacion: this.calificacionComic
      }
      this.$emit('crearComentario', comentario)
      this.limpiarInputs();
    }
  },
  beforeDestroy() {
  }
}
</script>

<style>
h1 {
  font-size: 2rem;
  font-weight: bold;
  margin-bottom: 25px;
}
.icono-refresh {
  position: absolute;
  top: 9vh;
  left: 61vw;
}

.icono-refresh:hover {
  cursor: pointer;
}

.card-comic {
  max-height: 90vh;
  max-width: 100%;
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-gap: 5px;
  padding: 14px;
  border: 1px solid transparent;
  border-radius: 20px;
  -webkit-box-shadow: 6px 6px 18px -8px rgba(0, 0, 0, 0.75);
  -moz-box-shadow: 6px 6px 18px -8px rgba(0, 0, 0, 0.75);
  box-shadow: 6px 6px 18px -8px rgba(0, 0, 0, 0.75);
}
.card-comic .cont-img-comic {
  width: 100%;
  height: 100%;
}
.card-comic .cont-img-comic img {
  width: 100%;
  height: 100%;
  max-height: 90vh;
  object-fit: contain;
  object-position: center;
}
.card-comic .cont-info-comic {
  display: flex;
  flex-flow: row wrap;
  justify-content: center;
  align-content: flex-start;
  padding: 0 13px;
}
.card-comic .cont-info-comic .cont-title {
  text-align: center;
  height: fit-content;
}
.card-comic .cont-info-comic .descripcion-comic {
  padding: 0 15px;
  max-height: 29vh;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: inherit;
}
.card-comic .cont-info-comic .descripcion-comic p {
  height: 100%;
}
.card-comic .cont-info-comic .cont-comentario {
  padding: 0 16px;
  width: 100%;
}
.card-comic .cont-info-comic .cont-comentario textarea {
  width: 100%;
  height: 15vh;
  padding: 10px;
  border: 1px solid black;
}
.card-comic .cont-info-comic .cont-botones {
  width: 100%;
  display: flex;
  flex-flow: row wrap;
  justify-content: center;
  margin-top: 2vh;
}
.card-comic .cont-info-comic .cont-botones a {
  text-decoration: none;
  margin-right: 10px;
  width: auto;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 0 10px;
}

.btn {
  width: auto;
  height: 40px;
  font-weight: bold;
  color: #fff;
  border: 1px solid transparent;
  border-radius: 9px;
  box-shadow: 2px 3px 0px 0px rgba(0, 0, 0, 0.75);
}

.btn:hover {
  cursor: pointer;
  transform: translateY(-3px);
  transition: all 200ms ease-in-out;
}

.btn-danger {
  color: #fff;
  background-color: #e04141ed;
}

.btn-succes {
  color: #fff;
  background-color: #39a50ced;
}

.btn-danger:hover {
  background-color: #921c1ced;
}

.btn-succes:hover {
  background-color: #30921ced;
}

</style>
