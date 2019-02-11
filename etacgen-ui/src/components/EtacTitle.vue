<template>
  <span class="title" contenteditable v-on:input="titleChanged">{{title}}</span>
</template>

<script>
export default {
  name: 'EtacTitle',
  props: ['title'],
  methods: {
    titleChanged: function (evt) {
      // TODO: every change fires this, so probably debounce the title update
      // fire title update event
      this.$emit('title-changed', evt.target.innerText)
    }
  }
}
</script>

<style scoped>

</style>
