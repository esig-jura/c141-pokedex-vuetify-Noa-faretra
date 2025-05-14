<template>
  <v-container v-if="pokemon">
    <v-row>
      <v-col cols="12" md="4">
        <v-img contain height="300" :src="`/images/${pokemon.img}`" />
      </v-col>
      <v-col cols="12" md="8">
        <h1 class="text-h4">{{ pokemon.name }}</h1>
        <p>Niveau : {{ pokemon.level }}</p>
        <p>Types :
          <PokemonTypesChips class="mt-4" :pokemon="pokemon" />
        </p>
        <p class="mt-6 text-body-1">{{ pokemon.description }}</p>

        <!-- Placeholder pour stats -->
        <v-card class="mt-4">
          <v-card-title>Statistiques</v-card-title>
          <v-card-text>
            <PokemonStats class="mt-6" :stats="pokemon.stats" />
          </v-card-text>
        </v-card>
      </v-col>
    </v-row>
  </v-container>

  <v-container v-else>
    <v-alert class="text-center" type="error">
      Pokémon introuvable.
    </v-alert>
  </v-container>
</template>

<script setup>
  // Importation des bases
  import { useRoute } from 'vue-router'
  import { usePokemonStore } from '@/stores/pokemonStore'

  // Importation des composants
  import PokemonTypesChips from '@/components/PokemonTypesChips.vue'
  import PokemonStats from '@/components/PokemonStats.vue'

  // Récupération des données
  const route = useRoute()
  const pokemonStore = usePokemonStore()

  // Récupération de l'id du Pokémon
  const id = route.params.id
  const pokemon = pokemonStore.getPokemonById(id)

</script>

<style scoped>

</style>
