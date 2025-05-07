<template>
  <v-container>
    <h1 class="mb-6 text-center">Mes Pokémons Favoris</h1>

    <v-row v-if="favoris.length > 0">
      <v-col
        v-for="pokemon in favoris"
        :key="pokemon.id"
        cols="12"
        lg="3"
        md="4"
        sm="6"
        xl="2"
      >
        <PokemonCard :pokemon="pokemon" />
      </v-col>
    </v-row>

    <v-alert
      v-else
      class="text-center mt-4"
      type="info"
    >
      Vous n'avez pas encore de Pokémon favoris.<br>
      <v-btn to="/">Retourner à la liste</v-btn>
    </v-alert>
  </v-container>
</template>

<script setup>
  import { usePokemonStore } from '@/stores/pokemonStore'
  import PokemonCard from '@/components/PokemonCard.vue'

  const pokemonStore = usePokemonStore()
  const favoris = computed(() => pokemonStore.getFavorites)
</script>
