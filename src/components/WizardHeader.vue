<template>
  <div class="text-sm border-b border-gray-500 p-4 flex justify-between select-none">
    <div>Step: {{output}}</div>
    <div class="text-gray-600">Registration Form</div>
  </div>
</template>
<script>
import { computed, ref, toRef } from "vue"
export default {
  props: {
    step: { type: Number }
  },
  setup(props) {
    const step = toRef(props, 'step')
    const steps = ['username', 'email', 'review']
    const output = computed(() => {
      return steps[step.value - 1]
    })
    return { output }
  },
}
</script>