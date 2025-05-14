<template>
  <v-container>
    <v-sheet class="mx-auto bg-transparent" max-width="400">
      <h1 class="mb-4">Connexion</h1>
    </v-sheet>

    <!--
        Information de connexion
     -->
    <v-sheet class="pa-2 my-4">
      email: <code>sacha@pokemon.com</code> <br>
      password: <code>pika</code>
    </v-sheet>

    <v-form @submit.prevent="login">

      <v-text-field
        v-model="loginEmail"
        aria-label="Champ de saisie pour l'email"
        autofocus
        label="Email"
        required
        :rules="[validateEmail]"
        type="email"
      />

      <v-text-field
        v-model="loginPassword"
        aria-label="champe de saisie pour le mot de passe"
        label="Mot de passe"
        required
        :rules="[validatePassword]"
        type="password"
      />

      <v-alert
        v-if="errorMessage"
        border="start"
        class="mb-6"
        color="warning"
      >
        {{ errorMessage }}
      </v-alert>
      <v-btn
        aria-label="Bouton pour se connecter"
        color="primary"
        size="large"
        type="submit"
      >
        Se connecter
      </v-btn>
    </v-form>
  </v-container>
</template>

<script setup>
// Importation des dépendances nécessaires
  import { useAuthStore } from '@/stores/authStore'
  import { useRoute, useRouter } from 'vue-router'
  import { ref } from 'vue'

  // initialisation du router et de la route pour la direction
  const router = useRouter()
  const route = useRoute()

  // store d'authentification
  const authStore = useAuthStore()

  // donner reactive pour le formulaire
  const loginEmail = ref('')
  const loginPassword = ref('')

  // message d'erreur
  const errorMessage = ref('')

  // fonction de connexion
  function login () {
    const response = authStore.login(loginEmail.value, loginPassword.value)
    if (response.success) {
      router.push(route.query.redirect || '/')
    } else {
      errorMessage.value = response.message
    }
  }

  // regle de validation pour le champ email
  const validateEmail = email => {
    const emailPattern = /^[^\s@]+@[^\s@]+\.[^\s@]+$/
    return emailPattern.test(email) || 'Veuillez entrer un email valide'
  }

  // regle de validation pour le champ password
  const validatePassword = password => {
    return password.length > 3 || 'Le mot de passe doit contenir au moins 4 caractères'
  }
</script>

<style scoped>

</style>
