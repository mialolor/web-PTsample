<script setup>
import AppLayout from '@/components/layout/AppLayout.vue'
import LoginForm from '@/components/auth/LoginForm.vue'
import { useDisplay } from 'vuetify'

const { mobile } = useDisplay()
</script>

<template>
  <AppLayout :is-with-app-bar-nav-icon="false">
    <template #content>
      <v-container fluid>
        <v-row>
        <v-col cols="12" lg="8" class="bg-surface-light h-screen" v-if="!mobile"></v-col>
          <v-col cols="12" md="4" class="mx-auto pt-16">
            <v-card class="mx-auto" elevation="24">
              <v-card-title class="text-center">
                <v-img
                  class="mx-auto mt-6"
                  src="/images/PawTrack Logo (3).png"
                  :width="mobile ? '60%' : '50%'"
                  style="border-radius: 50%; overflow: hidden"
                ></v-img>

                <h3 class="font-weight-black text-center">PawTrack</h3>
                <p class="font-weight-bold mb-5">Login Form</p>
              </v-card-title>

              <v-card-text class="bg-surface-light pt-4">
                <v-divider class="my-5"></v-divider>

                <LoginForm></LoginForm>

                <v-divider class="my-5"></v-divider>

                <h5 class="text-center">
                  Don't have account?
                  <RouterLink
                    class="text-yellow-darken-4 font-weight-black"
                    to="/register"
                    >Click here to Register</RouterLink
                  >
                </h5>
              </v-card-text>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </template>
  </AppLayout>
</template>
