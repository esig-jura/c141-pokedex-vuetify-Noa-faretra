<template>
  <router-link class="text-decoration-none" :to="`/pokemon/${pokemon.id}`">
    <v-card class="pa-2" elevation="2">
      <v-img contain height="200" :src="`/images/${pokemon.img}`" />
      <v-card-title class="text-h6">{{ pokemon.name }}</v-card-title>
      <v-card-subtitle>Niveau : {{ pokemon.level }}</v-card-subtitle>
      <v-btn
        class="position-absolute top-0 right-0 mt-2 mr-2"
        icon
        variant="plain"
        @click.prevent="pokemonStore.toggleFavorite(pokemon)"
      >
        <v-icon :color="pokemonStore.isFavorite(pokemon) ? 'red' : ''">
          {{ pokemonStore.isFavorite(pokemon) ? 'mdi-heart' : 'mdi-heart-outline' }}
        </v-icon>
      </v-btn>
    <!-- À compléter plus tard avec les types -->
    </v-card>
  </router-link>
</template>

<script setup>
  import { usePokemonStore } from '@/stores/pokemonStore'
  const pokemonStore = usePokemonStore()

  defineProps({
    pokemon: Object,
  })
</script>

<style scoped>

</style>
