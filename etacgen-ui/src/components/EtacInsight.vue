<template>
  <div class="insight">
    <h4 class="horizontal layout center">
      <i class="material-icons">{{icon}}</i>
      {{ title }}
    </h4>
    <div class="observations" v-if="observations.length > 0">
      <etac-observation
        v-for="observation in observations"
        v-on:observation-removed="removeObservation"
        :key="observation.text"
        :observation="observation">
      </etac-observation>
    </div>
    <div class="emptyset" v-else>
    </div>
    <button @click="addObservation">Add {{title}}</button>
  </div>
</template>

<script>

import EtacObservation from '@/components/EtacObservation'

export default {
  name: 'EtacInsight',
  props: [ 'title', 'icon', 'section', 'insight', 'observations' ],
  components: { EtacObservation },
  methods: {
    addObservation () {
      this.$emit('observation-added', {
        section: this.section,
        insight: this.insight,
        text: `New observation`
      })
    },
    removeObservation (observation) {
      this.$emit('observation-removed', observation)
    }
  }
}
</script>

<style scoped lang="scss">
  $opportunity-color: rgb(110, 175, 202);
  $impact-color: rgb(107, 150, 120);
  $techfeas-color: rgb(218, 189, 128);

  .insight {
    margin: 0 1rem;
    min-height: 5rem;
    text-align: left;
  }

  .insight.opportunity {
    color: $opportunity-color;
    border-bottom: solid 1px $opportunity-color;
  }

  .insight.impact {
    color: $impact-color;
    border-bottom: solid 1px $impact-color;
  }

  .insight.techfeas {
    color: $techfeas-color;
    border-bottom: solid 1px $techfeas-color;
  }

  h4 { padding: 0.5rem; margin: 0; }

</style>
