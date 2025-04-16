<template>
  <div
    class="v-container v-locale--is-ltr"
    style="max-width: 600px"
  >
    <h1 class="mb-6 text-center">Le Monde Pokémon</h1>
    <div aria-label="Carte du monde Pokémon" class="v-responsive v-img mb-6 cursor-pointer" role="img">
      <v-img
        alt="Carte du monde Pokémon"
        class="v-img__img v-img__img--contain"
        max-width="600"
        :src="imageUrl"
        @click="dialog =true"
      />
    </div>
    <v-dialog
      v-model="dialog"
      fullscreen
      hide-overlay
      persistent
      transition="dialog-bottom-transition"
    >
      <div
        class="d-flex align-center justify-center fill-height"
        style="background-color: rgba(0, 0, 0, 0.9)"
        @click.self="dialog = false"
      />

      <v-img
        class=" elevation-4"
        max-height="90%"
        max-width="90%"
        :src="imageUrl"
      />
      <v-btn
        class="close-btn"
        text="Fermer"
        @click="dialog = false"
      />
    </v-dialog>

    <v-card>
      <v-card-text>
        <v-card-title><h2>Un univers fascinant à découvrir</h2></v-card-title>
        <v-card-text>
          <p>Le monde Pokémon est un vaste et merveilleux univers peuplé de créatures extraordinaires appelées Pokémon.
            Cette carte représente les différentes régions que les dresseurs peuvent explorer, chacune offrant ses propres
            défis, Pokémon uniques et aventures palpitantes.</p>
        </v-card-text>

        <v-card-title><h2>Des régions diversifiées</h2></v-card-title>
        <v-card-text>
          <p>De Kanto à Galar, en passant par Johto, Hoenn, Sinnoh, Unova, Kalos et Alola, chaque région du monde
            Pokémon possède sa propre identité, sa culture et son écosystème unique. Les paysages varient des montagnes
            enneigées aux îles tropicales, offrant une diversité incroyable d'habitats pour
            les différentes espèces de Pokémon.</p>
        </v-card-text>

        <v-card-title><h2>Un monde en constante évolution</h2></v-card-title>
        <v-card-text>
          <p>Le monde Pokémon est en perpétuelle expansion, avec de nouvelles régions, de nouvelles espèces de
            Pokémon et de nouvelles aventures qui sont régulièrement découvertes. Cette carte n'est qu'un aperçu
            d'un univers riche et en constante évolution, prêt à être exploré par les dresseurs audacieux.</p>
        </v-card-text>

        <v-card-title><h2>Un appel à l'aventure</h2></v-card-title>
        <v-card-text>
          <p>Que vous soyez un dresseur débutant ou expérimenté, le monde Pokémon vous invite à partir à l'aventure.
            Capturez de nouveaux Pokémon, affrontez des champions d'arènes, déjouez les plans des équipes malveillantes
            et devenez peut-être le prochain Maître Pokémon. L'aventure commence ici, sur cette carte,
            mais où vous mènera-t-elle ?</p>
        </v-card-text>
      </v-card-text>
    </v-card>
  </div>
</template>

<script setup>
  import { ref } from 'vue'

  const dialog = ref(false)
  const imageUrl = '/images/pokemon-map.png'
</script>

<style scoped>
.cursor-pointer {
  cursor: pointer;
}
</style>
