<template>
  <div class="text-h4 text-blue-darken-4 pl-5 pt-10">Encourage sharing</div>
  <v-container class="pa-lg-15" fluid>
    <v-alert v-if="saveStatus != 'none' && saveStatus == 'success'" class="mb-5" type="success"
      title="Thank you for your contribution" text="your message has been saved successfully"></v-alert>
    <v-alert v-if="saveStatus != 'none' && saveStatus == 'failed'" class="mb-5" type="error" title="FAILED"
      text="something went wrong"></v-alert>
    <v-form ref="form" fast-fail @submit.prevent="submitMessage">
      <v-textarea clearable clear-icon="mdi-close-circle" counter label="Message" :rules="rules"
        v-model="message"></v-textarea>
      <v-btn class="me-4" type="summit">
        submit
      </v-btn>
    </v-form>
  </v-container>
</template>
<script setup lang="ts">
import type { Encourage } from '~/types'
const { create } = useStrapi()

const rules = [
  v => v.length <= 150 || 'Max 150 characters',
  v => v.length > 0 || 'Please enter message',
  v => v?.trim() != "" || 'Please enter message',
]

const form = ref(null)
const message = ref("")
const saveStatus = ref("none")
async function submitMessage() {
  const { valid } = await form.value?.validate()
  if (valid) {
    try {
      const result = await create<Encourage>('encourages', { message: message.value })
      form?.value.reset()
      saveStatus.value = "success"
    } catch {
      saveStatus.value = "failed"
    }

    setTimeout(() => {
      saveStatus.value = "none"
    }, 3000)
  }
}
</script>
