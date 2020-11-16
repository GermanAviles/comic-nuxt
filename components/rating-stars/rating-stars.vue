<template>
  <div class="rating-box">
    <div class="rating-container">
      <input id="star-5" type="radio" name="rating" value="5" @input="cambiarValue($event)"> <label for="star-5">&#9733;</label>
      <input id="star-4" type="radio" name="rating" value="4" @input="cambiarValue($event)"> <label for="star-4">&#9733;</label>
      <input id="star-3" type="radio" name="rating" value="3" @input="cambiarValue($event)"> <label for="star-3">&#9733;</label>
      <input id="star-2" type="radio" name="rating" value="2" @input="cambiarValue($event)"> <label for="star-2">&#9733;</label>
      <input id="star-1" type="radio" name="rating" value="1" @input="cambiarValue($event)"> <label for="star-1">&#9733;</label>
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
  },
  data: () => ({}),

  computed: {
  },

  watch: { },

  mounted() {
    this.$root.$on('reiniciarnputs', () => {
      this.resetStars()
    })
  },

  created() {
  },

  methods: {
    cambiarValue( event ) {
      this.$emit('rating', event.target.value);
    },
    resetStars() {
      document.getElementById('star-5').checked = false
      document.getElementById('star-4').checked = false
      document.getElementById('star-3').checked = false
      document.getElementById('star-2').checked = false
      document.getElementById('star-1').checked = false
    }
  },
  beforeDestroy() {
  }
}
</script>

<style>
.rating-box {
  display: inline-block;
  height: fit-content;
}
.rating-box .rating-container {
  direction: rtl !important;
}
.rating-box .rating-container label {
  display: inline-block;
  margin: 15px 0;
  color: #d4d4d4;
  cursor: pointer;
  font-size: 50px;
  transition: color 0.2s;
}
.rating-box .rating-container input {
  display: none;
}
.rating-box .rating-container label:hover, .rating-box .rating-container label:hover ~ label, .rating-box .rating-container input:checked ~ label {
  color: gold;
}

/*# sourceMappingURL=probando.css.map */

</style>
