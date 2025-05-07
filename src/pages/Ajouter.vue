<template>
  <v-container>
    <h1 class="mb-6 text-center">Ajouter un Pokémon</h1>

    <v-form @submit.prevent="submitForm">
      <v-text-field v-model="name" label="Nom du Pokémon" required />
      <v-text-field v-model="img" label="Nom de l'image (.png)" required />
      <v-text-field v-model.number="level" label="Niveau" required type="number" />

      <v-btn color="primary" type="submit">Ajouter</v-btn>
    </v-form>
  </v-container>
</template>

<script setup>
  import { ref } from 'vue'
  import { usePokemonStore } from '@/stores/pokemonStore'

  const pokemonStore = usePokemonStore()

  const name = ref('')
  const img = ref('')
  const level = ref(1)

  function submitForm () {
    const newPokemon = {
      name: name.value,
      img: img.value,
      level: level.value,
      types: [],
      hp: 50,
      attack: 50,
      defense: 50,
      speed: 50,
    }

    pokemonStore.addPokemon(newPokemon)

    // Réinitialisation du formulaire
    name.value = ''
    img.value = ''
    level.value = 1
  }
</script>
