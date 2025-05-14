<template>
  <!--
  Barre d'application plate
    * flat supprime l'ombre sous la barre
  -->
  <v-app-bar flat>
    <!--
    Conteneur de la barre d'application
      * class="d-flex align-start align-center" aligne les éléments de manière flexible, alignés en haut et centrés verticalement
    -->
    <v-container class="d-flex align-start align-center">
      <!--
      Logo de l'application cliquable
        * class="mr-4 pa-0 cursor-pointer" ajoute une marge à droite, retire le padding, et change le curseur pour indiquer la cliquabilité
        * image définit le chemin vers le logo (Pokeball) de l'application
        * size="64" définit la taille de l'avatar
        * @click redirige vers la page d'accueil
      -->
      <v-avatar
        class="mr-4 pa-0 cursor-pointer"
        image="@/assets/pokeball.svg"
        size="64"
        @click="$router.push('/')"
      />

      <!-- Titre de l'application affiché dans la barre -->
      <v-toolbar-title>Pokedex : {{ pokemonStore.totalPokemons }} / 255</v-toolbar-title>

      <!--
      Liens de navigation générés dynamiquement
        * v-for parcourt chaque élément dans menuItems pour créer un lien de navigation
        * :key utilise link.title pour définir une clé unique par lien
        * :icon affiche l'icône spécifiée pour chaque lien
        * :to utilise le chemin vers la route spécifiée pour chaque lien
      -->
      <v-btn
        v-for="link in menuItems"
        :key="link.title"
        :icon="link.icon"
        :to="link.path"
      />

      <v-btn
        v-if="authStore.isAuthenticated"
        icon="mdi-logout"
        @click="logout"
      />

      <v-btn
        v-else
        icon="mdi-login"
        @click="$router.push('/login')"
      />
    </v-container>
  </v-app-bar>

  <v-snackbar
    v-model="snackbar"
    color="succes"
  >
    Déconnexion réussis !
  </v-snackbar>
</template>

<script setup>

// récuperer le magasin
  import { usePokemonStore } from '@/stores/pokemonStore'
  import { useAuthStore } from '@/stores/authStore'
  import router from '@/router'
  import { ref } from 'vue'

  const pokemonStore = usePokemonStore()
  const authStore = useAuthStore()

  /*
  Définition des éléments de menu pour la navigation
    - Chaque élément contient :
      * title : le titre du lien
      * path : le chemin de la route
      * icon : l'icône du lien
  */
  const menuItems = [
    { title: 'Accueil', path: '/', icon: 'mdi-pokeball' },
    { title: 'Favoris', path: '/Favoris', icon: 'mdi-heart' },
    { title: 'FAQ', path: '/FAQ', icon: 'mdi-frequently-asked-questions' },
    { title: 'KantoMap', path: '/KantoMap', icon: 'mdi-map' },
    // Ajouter ici les autres liens du menu.
    // Vous trouverez des icônes sur https://pictogrammers.com/library/mdi/
    // N'oubliez pas d'ajouter le préfixe 'mdi-' devant le nom de l'icône.
  ]

  // etat pour controler l'affichage du snackbar de deconnexion
  const snackbar = ref(false)

  // fonction de déconnexion
  function logout () {
    snackbar.value = true // afficher le snackbar
    authStore.logout() // déconnexion
    router.push('/') // rediriger vers la page d'accueil
  }
</script>
