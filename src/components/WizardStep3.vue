<template>
  <div class="leading-loose">
    <p>Please review these details befor completing registration proccess:</p>
    <p>Username: {{formData.username}}</p>
    <p>Email: {{formData.email}}</p>
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

    const validateStep = function() {
      return true
    }
    return { formData, validateStep }
  },
}
</script>