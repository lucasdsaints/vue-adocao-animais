<template>
  <div class="home">
    <h1>Adopt a new best friend.</h1>
    <b-button variant="primary" @click="togglePetForm" v-if="!showPetForm">Add New Pet</b-button>
    <b-button variant="primary" @click="togglePetForm" v-if="showPetForm">Cancel</b-button>

    <b-form @submit.prevent="handleSubmit" v-if="showPetForm">
      <b-form-group id="name-input-group" label="Pet's Name:" label-for="name-input">
        <b-form-input
          id="name-input"
          v-model="formData.name"
          required
          placeholder="Enter name"
        ></b-form-input>
      </b-form-group>

      <b-form-group id="specie-input-group" label="Species:" label-for="specie-input">
        <b-form-select
          id="species-input"
          v-model="formData.species"
          :options="['cats', 'dogs']"
          required
        ></b-form-select>
      </b-form-group>

      <b-form-group id="pet-age-input-group" label="Pet's Age:" label-for="pet-age-input">
        <b-form-input
          id="pet-age-input"
          type="number"
          v-model="formData.age"
          required
          placeholder="Enter age"
        ></b-form-input>
      </b-form-group>

      <b-button type="submit" variant="primary">Submit</b-button>
      <b-button type="reset" variant="danger">Reset</b-button>
    </b-form>
  </div>
</template>

<script>
import { mapActions } from 'vuex'

export default {
  name: 'Home',
  data () {
    return {
      showPetForm: false,
      formData: {
        name: '',
        age: 0,
        species: null
      }
    }
  },
  methods: {
    ...mapActions([
      'addPet'
    ]),
    togglePetForm () {
      this.showPetForm = !this.showPetForm
    },
    handleSubmit () {
      const { species, name, age } = this.formData
      const payload = {
        species,
        pet: {
          name,
          age
        }
      }
      this.addPet(payload)
      this.formData = {
        name: '',
        age: 0,
        species: null
      }
    }
  }
}
</script>
