<template>
  <!--
  Conteneur principal de l'application utilisant Vuetify
    * <v-app> est l'enveloppe principale pour l'intégration des composants Vuetify
  -->
  <v-app>
    <!--
    Menu principal
      * Affiche la barre de navigation principale (header)
      * Inclut le composant personnalisé MenuPrincipal créer dans le fichier `src/components/AppHeader.vue`
    -->
    <menu-principal />
    <!--
    Section principale de l'application
      * <v-main> définit le conteneur principal pour afficher le contenu de l'application
      * <router-view> est une zone de rendu dynamique utilisée par Vue Router
        pour afficher les composants des routes actuelles
    -->
    <v-main>
      <router-view />
    </v-main>
    <!--
    Pied de page de l'application
      * <v-footer> : Composant Vuetify pour un pied de page réactif et stylisé.
      * <div> : Conteneur pour le contenu du pied de page.
        - class="px-4" : Ajoute un padding horizontal (4 * 4px = 16px) pour espacer le contenu des bords.
        - class="text-center" : Centre le texte horizontalement.
        - class="w-100" : Assure que le conteneur occupe toute la largeur disponible.
    -->
    <v-footer>
      <div class="px-4 text-center w-100">2025 - Pokedex</div>
    </v-footer>
  </v-app>
</template>

<script setup>
  // Importation du composant MenuPrincipal pour l'en-tête de l'application
  import MenuPrincipal from '@/components/AppHeader.vue'
  import { usePokemonStore } from '@/stores/pokemonStore'

  const magasinPokemon = usePokemonStore()

  // Lorsque le composant est monté, charger les favoris
  onMounted(() => {
    magasinPokemon.loadFavorites()
  })
</script>
