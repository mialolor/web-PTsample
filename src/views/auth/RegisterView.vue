<script setup>
import AppLayout from '@/components/layout/AppLayout.vue'
import RegisterForm from '@/components/auth/RegisterForm.vue'
import { useDisplay } from 'vuetify'

const { mobile } = useDisplay()
</script>

<template>
  <AppLayout :is-with-app-bar-nav-icon="false">
    <template #content>
      <v-container fluid>
        <v-row>
          <v-col cols="12" lg="8" class="bg-surface-light h-screen" v-if="!mobile">
            <v-img src="/images/haha.PNG"
          :width="'100%'"
          :height="'100%'"
          >
              </v-img>
            </v-col>
          <v-col cols="12" md="4" class="mx-auto pt-16">
            <v-card class="mx-auto" elevation="24"
              ><v-card-title class="text-center">
                <v-img
                  class="mx-auto mt-6"
                  src="/images/PawTrack Logo (3).png"
                  :width="mobile ? '60%' : '40%'"
                  style="border-radius: 50%; overflow: hidden"
                ></v-img>
                <h3 class="font-weight-black text-center">PawTrack</h3>
                <p class="mb-5"><b>Registration Form</b></p>
              </v-card-title>

              <v-card-text class="bg-surface-light pt-4">
                <v-divider class="my-5"></v-divider>

                <RegisterForm></RegisterForm>

                <v-divider class="my-5"></v-divider>

                <h4 class="text-center">
                  Already have account?
                  <RouterLink
                    class="text-yellow-darken-4 font-weight-black"
                    to="/"
                    >Click here to Login</RouterLink
                  >
                </h4>
              </v-card-text>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </template>
  </AppLayout>
</template>
