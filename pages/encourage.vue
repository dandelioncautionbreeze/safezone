<template>
  <div class="text-h4 text-blue-darken-4 pl-5 pt-10">Encourages <v-btn icon="mdi-plus" size="small"
      to="/add-encourage"></v-btn></div>

  <v-carousel class="pt-10" cycle height="520" hide-delimiter-background :show-arrows="false">
    <v-carousel-item v-for="({ attributes, id }, i) in encourages.data" :key="i">
      <div class="ma-sm-10"><v-card>
          <v-img :src="photos[i % photos.length]" class="align-end" gradient="to bottom, rgba(0,0,0,.1), rgba(0,0,0,.5)"
            height="240pt" cover>
            <v-row>
              <v-col class="text-white text-lg-h2 text-md-h2 text-sm-h4 pa-10">
                {{ attributes.message}}
              </v-col>
            </v-row>
          </v-img>

          <v-card-actions>
            <v-spacer></v-spacer>
            {{ attributes.heart }}
            <v-btn size="small" color="red" variant="text" icon="mdi-heart" @click="bumpHeart(id, attributes)"></v-btn>
          </v-card-actions>
        </v-card></div>

    </v-carousel-item>
  </v-carousel>
</template>
<script setup lang="ts">
import { Encourage } from '~/types'
const { find, update } = useStrapi()
const encourages = ref(null)
encourages.value = await find<Encourage>('encourages')
const photos = [
  'https://cdn.pixabay.com/photo/2016/02/27/18/07/clover-1225988_960_720.jpg',
  'https://cdn.pixabay.com/photo/2017/08/01/08/16/couple-2563424_960_720.jpg',
  'https://cdn.pixabay.com/photo/2017/11/26/15/16/smiley-2979107_960_720.jpg',
  'https://cdn.pixabay.com/photo/2015/05/11/14/51/heart-762564_640.jpg',
  'https://cdn.pixabay.com/photo/2019/09/13/17/58/unicorns-4474543_960_720.jpg',
  'https://cdn.pixabay.com/photo/2017/10/23/21/13/soap-bubbles-2882599_960_720.jpg',
  'https://cdn.pixabay.com/photo/2016/03/26/22/22/happy-1281590_960_720.jpg',
  'https://cdn.pixabay.com/photo/2015/10/19/15/17/plush-996216_960_720.jpg',
]
async function bumpHeart(id, attributes) {
  const heart = Number(attributes.heart) + 1
  const message = attributes.message
  const result = await update<Encourage>('encourages', id, {
    message: message,
    heart: heart,
  })
  encourages.value = await find<Encourage>('encourages')
}
</script>