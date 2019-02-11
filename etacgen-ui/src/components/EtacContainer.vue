<template>
<div id="etac">
  <button v-on:click="clearData">Clear Data</button>
  <h1 contenteditable v-on:blur="titleChanged" v-on:keydown="checkForEnter">{{title}}</h1>
  <section id="observations" class="vertical layout">
    <div class="horizontal layout">
      <section id="opportunity" class="vertical layout flex-auto opportunity">
        <h2>Opportunity</h2>
        <etac-insight
          title="Trigger"
          icon="whatshot"
          section="opportunity"
          insight="triggers"
          class="opportunity"
          :observations="observationsFor('opportunity', 'triggers')"
          v-on:observation-added="observationAdded"
          v-on:observation-removed="observationRemoved">
        </etac-insight>
        <etac-insight
          title="Players"
          icon="people"
          section="opportunity"
          insight="players"
          class="opportunity"
          :observations="observationsFor('opportunity', 'players')"
          v-on:observation-added="observationAdded"
          v-on:observation-removed="observationRemoved">
        </etac-insight>
        <etac-insight
          title="Drivers"
          icon="arrow_forward"
          class="opportunity"
          section="opportunity"
          insight="drivers"
          :observations="observationsFor('opportunity', 'drivers')"
          v-on:observation-added="observationAdded"
          v-on:observation-removed="observationRemoved">
        </etac-insight>
      </section>
      <section id="impact" class="vertical layout flex-auto impact">
        <h2>Impact</h2>
        <div class="horizontal layout flex-auto">
          <section id="macro" class="vertical layout flex-auto">
            <h3>Macro</h3>
            <etac-insight
              title="Network Effects &amp; Interactions"
              icon="people_outline"
              class="impact"
              section="impactmicro"
              insight="networkeffects"
              :observations="observationsFor('impactmicro', 'networkeffects')"
              v-on:observation-added="observationAdded"
              v-on:observation-removed="observationRemoved">
            </etac-insight>
            <etac-insight
              title="Disruptees"
              icon="offline_bolt"
              class="impact"
              section="impactmicro"
              insight="disruptees"
              :observations="observationsFor('impactmicro', 'disruptees')"
              v-on:observation-added="observationAdded"
              v-on:observation-removed="observationRemoved">
            </etac-insight>
          </section>
          <section id="micro" class="vertical layout flex-auto">
            <h3>Micro</h3>
            <etac-insight
              title="Competitive Advantage"
              icon="trending_up"
              class="impact"
              section="impactmacro"
              insight="compadvantages"
              :observations="observationsFor('impactmacro', 'compadvantages')"
              v-on:observation-added="observationAdded"
              v-on:observation-removed="observationRemoved">
            </etac-insight>
            <etac-insight
              title="Financial Benefits"
              icon="monetization_on"
              class="impact"
              section="impactmacro"
              insight="financialbenefits"
              :observations="observationsFor('impactmacro', 'financialbenefits')"
              v-on:observation-added="observationAdded"
              v-on:observation-removed="observationRemoved">
            </etac-insight>
            <etac-insight
              title="Supply Chain"
              icon="local_shipping"
              class="impact"
              section="impactmacro"
              insight="supplychains"
              :observations="observationsFor('impactmacro', 'supplychains')"
              v-on:observation-added="observationAdded"
              v-on:observation-removed="observationRemoved">
            </etac-insight>
          </section>
        </div>
      </section>
      <section id="feasibility" class="vertical layout flex-auto techfeas">
        <h2>Technical Feasibility</h2>
        <etac-insight
          title="Technical Merit"
          icon="local_activity"
          class="techfeas"
          section="feasibility"
          insight="technicalmerits"
          :observations="observationsFor('feasibility', 'technicalmerits')"
          v-on:observation-added="observationAdded"
          v-on:observation-removed="observationRemoved">
          </etac-insight>
        <etac-insight
          title="Tools, Ecosystem, &amp; Skills"
          icon="build"
          class="techfeas"
          section="feasibility"
          insight="toolsecoskills"
          :observations="observationsFor('feasibility', 'toolsecoskills')"
          v-on:observation-added="observationAdded"
          v-on:observation-removed="observationRemoved">
        </etac-insight>
        <etac-insight
          title="Friction"
          icon="compare_arrows"
          class="techfeas"
          section="feasibility"
          insight="frictions"
          :observations="observationsFor('feasibility', 'frictions')"
          v-on:observation-added="observationAdded"
          v-on:observation-removed="observationRemoved">
        </etac-insight>
      </section>
    </div>
  </section>
  <section id="future" class="future">
    <h2>Future</h2>
    <div class="horizontal layout">
      <etac-insight
        title="Timeline"
        icon="whatshot"
        section="future"
        insight="timeline"
        class="timeline flex-auto"
        :observations="observationsFor('future', 'timeline')"
        v-on:observation-added="observationAdded"
        v-on:observation-removed="observationRemoved">
      </etac-insight>
      <etac-insight
        title="Risks"
        icon="whatshot"
        section="future"
        insight="risks"
        class="risks flex-auto"
        :observations="observationsFor('future', 'risks')"
        v-on:observation-added="observationAdded"
        v-on:observation-removed="observationRemoved">
      </etac-insight>
    </div>
  </section>
  <section id="summary" class="summary">
    <h2>Summary</h2>
    <etac-insight
      title=""
      icon=""
      section="summary"
      insight="content"
      class="summary"
      :observations="observationsFor('summary', 'content')"
      v-on:observation-added="observationAdded"
      v-on:observation-removed="observationRemoved">
    </etac-insight>
  </section>
</div>
</template>

<script>
import EtacInsight from '@/components/EtacInsight'
import EtacTitle from '@/components/EtacTitle'

export default {
  name: 'EtacContainer',
  components: { EtacInsight, EtacTitle },
  data: () => {
    let title = localStorage.getItem('title') || '[INSERT TITLE]'
    let observations = localStorage.getItem('observations')

    if (!observations) {
      observations = {
        opportunity: {
          triggers: [],
          players: [],
          drivers: []
        },
        impactmicro: {
          networkeffects: [],
          disruptees: []
        },
        impactmacro: {
          compadvantages: [],
          financialbenefits: [],
          supplychains: []
        },
        feasibility: {
          technicalmerits: [],
          toolsecoskills: [],
          frictions: []
        },
        future: {
          timeline: [],
          risks: []
        },
        summary: {
          content: []
        }
      }
    } else {
      observations = JSON.parse(observations)
    }

    return {
      title: title,
      observations: observations
    }
  },
  watch: {
    title: {
      handler (newval, oldval) {
        localStorage.setItem('title', newval)
      }
    },
    observations: {
      handler (newval, oldval) {
        console.log('committing changes')
        localStorage.setItem('observations', JSON.stringify(newval))
      },
      deep: true
    }
  },
  methods: {
    titleChanged (evt) {
      this.title = evt.target.innerText
    },
    observationAdded (observation) {
      this.observations[observation.section][observation.insight].push(observation)
    },
    observationRemoved (observation) {
      let index = this.observations[observation.section][observation.insight].findIndex(o => o === observation)
      if (index !== -1) {
        this.observations[observation.section][observation.insight].splice(index, 1)
      }
    },
    observationsFor (section, insight) {
      return this.observations[section][insight]
    },
    checkForEnter (evt) {
      if (evt.which === 13) {
        evt.target.blur()
      }
    },
    clearData () {
      this.observations = {
        opportunity: {
          triggers: [],
          players: [],
          drivers: []
        },
        impactmicro: {
          networkeffects: [],
          disruptees: []
        },
        impactmacro: {
          compadvantages: [],
          financialbenefits: [],
          supplychains: []
        },
        feasibility: {
          technicalmerits: [],
          toolsecoskills: [],
          frictions: []
        }
      }
      this.title = '[INSERT TITLE]'
    }
  }
}
</script>

<style scoped lang="scss">
h1 { white-space: nowrap; }

h2 {
  color: #fff;
  text-transform: uppercase;
  font-weight: 600;
  height: 4rem;
}

.opportunity h2 {
  background-color: rgb(110, 175, 202);
}

.techfeas h2 {
  background-color: rgb(218, 189, 128);
}

.summary {
  h2 {
    background-color: rgb(100, 100, 100);
  }
}

.future {
  h2 {
    background-color: rgb(100, 100, 100);
  }
}

.impact {
  h2, h3 {
    background-color: rgb(107, 150, 120);
    height: 2rem;
  }
  h3 {
    background-color: rgb(138, 177, 129);
    color: #fff;
  }
}

</style>
