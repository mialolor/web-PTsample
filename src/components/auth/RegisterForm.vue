<script setup>
import {
  requiredValidator,
  emailValidator,
  passwordValidator,
  confirmedValidator,
} from '@/utils/validators'
import { ref } from 'vue'
import { supabase, formActionDefault } from '@/utils/supabase.js'

const formDataDefault = {
  firstname: '',
  lastname: '',
  email: '', 
  password: '',
  password_confirmation: '',
}

const formData = ref({
  ...formDataDefault,
})

const formAction = ref({
  ...formActionDefault,
})

const isPasswordVisible = ref(false)
const isPasswordConfirmVisible = ref(false)
const refVForm = ref()

const onSubmit = async () => {
  formAction.value = { ...formActionDefault }
  formAction.value.formProcess = true

  const { data, error } = await supabase.auth.signUp({
    email: formData.value.email,
    password: formData.value.password,
    options: {
      data: {
        firstname: formData.value.firstname,
        lastname: formData.value.lastname,
      },
    },
  })

  if (error) {
    console.log(error)
    formAction.value.formErrorMessage = error.message
    formAction.value.formStatus = error.status
  } else if (data) {
    console.log(data)
    formAction.value.formSuccessMessage = 'Successfully Rehgistered Account.'
    // Add here more action sif you want
  }

  formAction.value.formProcess = false
}

const onFormSubmit = () => {
  refVForm.value?.validate().then(({ valid }) => {
    if (valid) onSubmit()
  })
}
</script>

//@v-on event
<template>
  <v-alert
    v-if="formAction.formSuccessMessage"
    :text="formAction.formSuccessMessage"
    title="Success"
    type="success"
    variant="tonal"
    density="compact"
    border="start"
    closable
  ></v-alert>

  <v-alert
    v-if="formAction.formErrorMessage"
    :text="formAction.formErrorsMessage"
    title="Ooops1"
    type="error"
    variant="tonal"
    density="compact"
    border="start"
    closable
  ></v-alert>

  <v-form ref="refVForm" @submit.prevent="onFormSubmit">
    <v-row>
      <v-col cols="12" md="6">
        <v-text-field
          v-model="formData.firstname"
          label="Firstname"
          prepend-inner-icon="mdi-account"
          :rules="[requiredValidator]"
        >
        </v-text-field>
      </v-col>

      <v-col cols="12" md="6">
        <v-text-field
          v-model="formData.lastname"
          label="Lastname"
          prepend-inner-icon="mdi-account"
          :rules="[requiredValidator]"
        >
        </v-text-field>
      </v-col>

      <v-col cols="12">
        <v-text-field
          v-model="formData.email"
          label="Email"
          prepend-inner-icon="mdi-email"
          :rules="[requiredValidator]"
        ></v-text-field>
      </v-col>

      <v-col cols="12" sm="6">
        <v-text-field
          prepend-inner-icon="mdi-lock"
          label="Password"
          :type="isPasswordVisible ? 'text' : 'password'"
          :append-inner-icon="isPasswordVisible ? 'mdi-eye-off' : 'mdi-eye'"
          @click:append-inner="isPasswordVisible = !isPasswordVisible"
          :rules="[requiredValidator, passwordValidator]"
        ></v-text-field>
      </v-col>

      <v-col cols="12" sm="6">
        <v-text-field
          v-model="formData.password_confirmation"
          label="Password Confirmation"
          :type="isPasswordConfirmVisible ? 'text' : 'password'"
          :append-inner-icon="
            isPasswordConfirmVisible ? 'mdi-eye-off' : 'mdi-eye'
          "
          @click:append-inner="
            isPasswordConfirmVisible = !isPasswordConfirmVisible
          "
          :rules="[
            requiredValidator,
            confirmedValidator(
              formData.password_confirmation,
              formData.password,
            ),
          ]"
        ></v-text-field>
      </v-col>
    </v-row>

    <v-btn
      class="mt-2 bg-yellow-darken-4"
      type="submit"
      block
      prepend-icon="mdi-account-plus"
      :disabled="formAction.formProcess"
      :loading="formAction.formProcess"
      >Register</v-btn
    >
  </v-form>
</template>
