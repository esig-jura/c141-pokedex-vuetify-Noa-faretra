<template>
  <v-container>
    <h1 class="mb-6 text-center">Pokédex</h1>

    <v-text-field
      v-model="search"
      clearable
      label="Rechercher un Pokémon"
      prepend-icon="mdi-magnify"
    />

    <v-row>
      <!-- Exemple de colonne vide (à dupliquer plus tard avec du contenu) -->
      <v-col
        v-for="pokemon in filteredPokemons"
        :key="pokemon.id"
        cols="12"
        lg="3"
        md="4"
        sm="6"
        xl="2"
        xs="12"
      >
        <PokemonCard :pokemon="pokemon" />
      </v-col>
    </v-row>
  </v-container>
</template>

<script setup lang="ts">
  // importation des bases
  import { computed, ref } from 'vue'

  // récupérer le composant card
  import PokemonCard from '@/components/PokemonCard.vue'

  // récuperer le magasin
  import { usePokemonStore } from '@/stores/pokemonStore'

  const pokemonStore = usePokemonStore()
  // console.log(pokemonStore.pokemons)

  // Variable de recherche
  const search = ref('')

  // Création d'une valeur calculer qui va check ce que l'utilisateur va entrer dans la barre de recherche
  const filteredPokemons = computed(() => {
    const query = search.value.toLowerCase().trim()
    return sortedPokemons.value.filter(pokemon =>
      pokemon.name.toLowerCase().includes(query)
    )
  })

  // Propriété pour trier les pokemons par odre alphabétique
  const sortedPokemons = computed(() => {
    return [...pokemonStore.pokemons].sort((a, b) =>
      a.name.localeCompare(b.name)
    )
  })
</script>

<style scoped>
.mdi-heart {
  animation : heartbeat 1s ease-in-out;
}
</style>
