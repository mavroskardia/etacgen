<template>
  <div :class="positiveOutlook ? 'observation positive' : 'observation negative'">
    <span contenteditable v-on:blur="commitChange" v-on:keypress="checkForEnter">{{observation.text}}</span>
    <button id="outlookBtn" @click="toggleOutlook">
      <i class="material-icons md-18">refresh</i>
    </button>
    <button id="removeBtn" @click="remove">
      <i class="material-icons">clear</i>
    </button>
  </div>
</template>

<script>
export default {
  name: 'EtacObservation',
  props: {
    observation: Object
  },
  data: () => ({
    positiveOutlook: true
  }),
  methods: {
    checkForEnter (evt) {
      if (evt.which === 13) {
        evt.target.blur()
      }
    },
    commitChange (evt) {
      this.observation.text = evt.target.innerText
    },
    toggleOutlook () {
      this.positiveOutlook = !this.positiveOutlook
    },
    remove () {
      this.$emit('observation-removed', this.observation)
    }
  }
}
</script>

<style lang="scss" scoped>
  $positive-color: rgb(198, 255, 207);
  $negative-color: rgb(255, 198, 207);

  .observation {
    position: relative;
    margin: 0.5rem;
    border: solid 1px green;
    border-radius: 4px;
    background-color: $positive-color;

    &.negative { background-color: $negative-color; }

    span {
      color: rgb(0, 54, 13);
      padding: 0.5rem;
      display: inline-block;
      white-space: nowrap;
      text-overflow: hidden;
    }

    button {
      position: absolute;
      right: 0;
      border: none;
      padding: 0;
      margin: 0;
      background-color: transparent;

      i { font-size: 18px; color: #555; }
      &#removeBtn { top: 0; }
      &#outlookBtn { bottom: 0; }
    }
  }
</style>
