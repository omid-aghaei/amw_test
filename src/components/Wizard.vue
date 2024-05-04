<template>
  <div class="w-screen max-w-xl h-96 bg-gray-100 border border-gray-500 rounded flex flex-col">
    <WizardHeader :step="step" />
    <div class="grow p-4 flex items-center justify-center">
      <WizardStep1 v-if="step === 1" ref="step_1" v-model="data" />
      <WizardStep2 v-if="step === 2" ref="step_2" v-model="data" />
      <WizardStep3 v-if="step === 3" ref="step_3" v-model="data" />
    </div>
    <div class="text-sm border-t border-gray-500 p-4 flex justify-between">
      <button id="btn-prev" class="bg-gray-700 text-white py-1 px-5 rounded transition duration-500 hover:bg-gray-900 disabled:bg-gray-300" :disabled="step < 2" @click="prev">Prev</button>
      <button id="btn-next" class="bg-gray-700 text-white py-1 px-5 rounded transition duration-500 hover:bg-gray-900 disabled:bg-gray-300" :disabled="step > 2" @click="validate">Next</button>
    </div>
  </div>
</template>
<script>
import { ref } from "vue"
import WizardHeader from './WizardHeader.vue'
import WizardStep1 from './WizardStep1.vue'
import WizardStep2 from './WizardStep2.vue'
import WizardStep3 from './WizardStep3.vue'
export default {
  components: { WizardHeader, WizardStep1, WizardStep2, WizardStep3 },
  setup() {
    const step = ref(1)
    const data = ref({ email: '', username: '' })

    const step_1 = ref(null)
    const step_2 = ref(null)
    const step_3 = ref(null)

    const next = function() { step.value ++ }
    const prev = function() { step.value -- }
    const validate = function() {
      if (step.value === 2 && step_2.value.validateStep()) { next() }
      if (step.value === 1 && step_1.value.validateStep()) { next() }
    }

    return {
      data, step,
      step_1, step_2, step_3,
      validate, prev
    }
  },
}
</script>