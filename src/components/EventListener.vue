<template >
  <div class="main_evnt">
    <input @input="arithmeticEvent" :type="type" :value="value" />
  </div>
</template>

<script>
export default {
  name: 'EventListener',
  props: {
    type: String,
    value: String
  },
  methods: {
    arithmeticEvent (event) {
      this.$emit('arithmetic', event)
    }
  }
}
</script>

<style scoped>
  input {
    align-items: center;
    padding: 5px;
    margin: 10px;
    text-align: center;
    width: 100px;
    border-radius: 10px;
    border-color: white;
  }
</style>

