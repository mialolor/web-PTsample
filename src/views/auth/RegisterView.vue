<script setup>
import AppLayout from '@/components/layout/AppLayout.vue'
import { useDisplay } from 'vuetify'

const { mobile } = useDisplay()
</script>

<template>
  <AppLayout>
    <template #content>
      <v-row>
        <v-col cols="12" md="6" class="mx-auto pt-16">
          <v-card class="mx-auto" elevation="24"
            ><v-card-title class="text-center">
              <v-img class="mx-auto" src="/images/logo-favicon.png"  :width="mobile ? '75%' : '50%'" ></v-img>
              <h3 class="font-weight-black text-center">PawTrack</h3>
              <p>RegistrationForm</p>
            </v-card-title>

            <v-card-text class="bg-surface-light pt-4">
              <v-form fast-fail @submit.prevent>
                <v-text-field label="Firstname" variant="outlined">
                </v-text-field>

                <v-text-field label="Lastname" variant="outlined">
                </v-text-field>

                <v-text-field label="Email" variant="outlined"> </v-text-field>

                <v-text-field
                  label="Password"
                  type="password"
                  variant="outlined"
                ></v-text-field>

                <v-text-field
                  label="Password Confirmation"
                  type="password"
                  variant="outlined"
                ></v-text-field>

                <v-btn
                  class="mt-2 bg-primary"
                  type="submit"
                  block
                  prepend-icon="mdi-account-plus"
                  >Register</v-btn
                >
              </v-form>

              <v-divider class="my-5"></v-divider>

              <h5 class="text-center">
                Already have account?
                <RouterLink class="text-primary" to="/"
                  >Click here to Login</RouterLink
                >
              </h5>
            </v-card-text>
          </v-card>
        </v-col>
      </v-row>
    </template>
  </AppLayout>
</template>
