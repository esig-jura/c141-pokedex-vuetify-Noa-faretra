<template>
  <v-container>
    <h1 class="mb-6 text-center">Pokédex</h1>

    <v-text-field
      clearable
      label="Rechercher un Pokémon"
      prepend-icon="mdi-magnify"
    />

    <v-row>
      <!-- Exemple de colonne vide (à dupliquer plus tard avec du contenu) -->
      <v-col
        v-for="pokemon in pokemonStore.pokemons"
        :key="pokemon.id"
        cols="12"
        lg="3"
        md="4"
        sm="6"
        xl="2"
        xs="12"
      >
        <v-card
          class="mx-auto"
          max-width="344"
        >
          <v-img
            :alt="pokemon.name"
            height="200px"
            :src="`/images/${pokemon.img}`"
          />

          <v-card-title>
            {{ pokemon.name }}
          </v-card-title>

          <v-card-subtitle>
            Niveau : {{ pokemon.level }}
          </v-card-subtitle>

          <v-card-actions>
            <v-btn
              color="red"
              :icon="pokemonStore.isFavorite(pokemon) ? 'mdi-heart' : 'mdi-heart-outline'"
              @click="pokemonStore.toggleFavorite(pokemon)"
            />
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script setup lang="ts">
 // récuperer le magasin
  import { usePokemonStore } from '@/stores/pokemonStore'

  const pokemonStore = usePokemonStore()
  // console.log(pokemonStore.pokemons)
</script>

<style scoped>
.mdi-heart {
  animation : heartbeat 1s ease-in-out;
}
</style>
