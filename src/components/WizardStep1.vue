<template>
  <div class="flex flex-col gap-2">
    <label for="username">Username:</label>
    <input type="text" name="username" id="username" v-model="formData.username" class="bg-gray-200 border border-gray-300 rounded px-2 py-1">
    <div v-if="error" class="text-sm text-red-500">Invalid Username.</div>
  </div>
</template>
<script>
import { computed, ref, toRef } from "vue"
export default {
  expose: ['validateStep'],
  props: {
    modelValue: { type: Object },
  },
  setup(props) {
    const formData = toRef(props, 'modelValue')
    const error = ref(false)

    const validateStep = function() {
      var format = /[ `!@#$%^&*()+\-=\[\]{};':"\\|,.<>\/?~]/;
      error.value = false
      if (formData.value.username === '') { error.value = true; return false } // epmty state
      if (format.test(formData.value.username)) { error.value = true; return false } // special characters
      if (formData.value.username.length < 4) { error.value = true; return false } // too short
      if (formData.value.username.length > 20) { error.value = true; return false } // too long
      return true
    }
    return { formData, validateStep, error }
  },
}
</script>