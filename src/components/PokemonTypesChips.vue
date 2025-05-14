<template>
  <div>
    <v-chip
      v-for="type in pokemonTypes"
      :key="type.id"
      class="ma-1"
      :color="type?.color || 'grey'"
      text-color="white"
    >
      {{ type?.name || 'inconnu' }}
    </v-chip>
  </div>
</template>

<script setup>
  import { computed, defineProps } from 'vue'
  import { usePokemonStore } from '@/stores/pokemonStore'

  const props = defineProps({
    pokemon: {
      type: Object,
      required: true,
    },
  })

  const store = usePokemonStore()

  const pokemonTypes = computed(() =>
    props.pokemon.types.map(id => store.getTypeById(id))
  )
</script>

<style scoped>

</style>
