<template>
  <v-app>
    <v-layout>
      <v-app-bar height="100pt" color="amber-lighten-5">
        <v-app-bar-title><v-img src="/images/gg.png" height="100pt"></v-img></v-app-bar-title>
      </v-app-bar>
      <v-main>
        <v-card color="basil" style="margin-top: 100pt">
          <v-tabs v-model="tab" bg-color="amber-lighten-4" color="basil" grow>
            <v-tab v-for="item in items" :key="item.name" :value="item.name" :to="item.link">
              <v-icon color="orange-accent-3" size="x-large">{{ item.icon }} </v-icon>
              {{ item.name }}
            </v-tab>
          </v-tabs>
        </v-card>
        <v-row>
          <v-col class="pa-5">
            <NuxtPage />
          </v-col>
        </v-row>
      </v-main>
    </v-layout>
  </v-app>
</template>
<script setup lang="ts">
const items = [
  { name: 'Home', icon: "mdi-home", link: "/" },
  { name: 'Encourage', icon: "mdi-heart", link: "/encourage" },
  { name: 'Expression', icon: "mdi-bird", link: "/expression" },
]
const tab = ref('HOME')
</script>