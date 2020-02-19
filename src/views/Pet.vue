<template>
  <div>
    <h1>{{ animal.name }} ({{ this.$route.params.species }})</h1>
    <p>Age: {{ animal.age }} years old</p>
    <p>Breed: {{ animal.breed }}</p>
  </div>
</template>

<script>
import { mapState } from 'vuex'

export default {
  data () {
    return {
      species: this.$route.params.species,
      id: this.$route.params.id,
      animal: {}
    }
  },
  computed: {
    ...mapState([
      'dogs',
      'cats'
    ])
  },
  mounted () {
    this.animal = this[this.$route.params.species][this.$route.params.id]
  }
}
</script>
