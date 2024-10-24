<script setup>
import { ref } from 'vue'

const theme = ref(localStorage.getItem('theme') ?? 'light')

function onClick() {
  theme.value = theme.value === 'light' ? 'dark' : 'light'
  localStorage.setItem('theme', theme.value)
}
</script>

<template>
  <v-responsive>
    <v-app :theme="theme">
      <v-app-bar
        class="px-3"
        :color="theme === 'light' ? 'amber-accent-3' : 'orange-lighten-1'"
        border
      >
        <v-spacer></v-spacer>

        <v-btn
        class="bg-yellow-darken-4"
          :icon="theme === 'light' ? 'mdi-weather-sunny' : 'mdi-weather-night'"
          variant="elevated"
          slim
          @click="onClick"
        ></v-btn>
      </v-app-bar>

      <v-main>
          <slot name="content"> </slot>
      </v-main>

      <v-footer
        class="font-weight-bold"
        :color="theme === 'light' ? 'brown-darken-3' : 'brown-darken-4'"
        elevation="24"
        border
        app
        >2024 - Copyright PawTrack
      </v-footer>
    </v-app>
  </v-responsive>
</template>
