<template>
    <div class="text-h4 text-blue-darken-4 pl-5 pt-10">Encourages  <v-btn icon="mdi-plus" size="small" to="/add-encourage"></v-btn></div>

    <v-carousel
     class="pt-10"
      cycle
      height="500"
      hide-delimiter-background
      show-arrows="hover"
    >
      <v-carousel-item
        v-for="({attributes}, i) in encourages.data"
        :key="i"
      >
        <v-sheet
          :color="colors[i % 5]"
          height="100%"
        >
          <div class="d-flex fill-height justify-center align-center">
            <div class="text-h2">
              {{ attributes.message }}
            </div>
          </div>
        </v-sheet>
      </v-carousel-item>
    </v-carousel>
</template>
<script setup lang="ts">
import type { Encourage } from '~/types'
const { find } = useStrapi()
const encourages = await find<Encourage>('encourages')
const colors = [
    'amber-lighten-2',
    'orange-lighten-2',
    'deep-orange-lighten-3',
    'pink-lighten-2',
    'purple-lighten-3',
]
</script>