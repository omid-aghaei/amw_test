<template>
  <div>
    <input id="description" v-model="text" @input="debouncer(() => isBalanced())" />
    <p>{{ result }}</p>
  </div>
</template>

<script>
export default {
  data() {
    return { text: "", result: '', debouncer: null }
  },
  methods: {
    createDebounce() {
    let timeout = null;
    return function (fnc, delayMs) { clearTimeout(timeout); timeout = setTimeout(() => { fnc() }, delayMs || 100) }
    },
    isBalanced() {
      let res = "The text is balanced."
      let openingChars = ["(", "[", "{"];
      let closingChars = [")", "]", "}"];
      for (let index = 0; index < openingChars.length; index++) {
        const a = this.text.split(openingChars[index]).length - 1
        const b = this.text.split(closingChars[index]).length - 1
        if (a !== b) { res = "The text is not balanced." }
      }
      this.result = res
    },
  },
  mounted () {
    this.debouncer = this.createDebounce()
  }
};
</script>