<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
      <div class="d-flex">
        Double Calculator
      </div>
    </v-app-bar>

    <v-main>
      <v-container v-bind:style="{ maxWidth: 'none' }">
        <v-row class="text-center justify-center">
          <v-col cols="3">
            <Calculator name="Calculator A" @add-history="addHistory" />
          </v-col>
          <v-col cols="3">
            <Calculator name="Calculator B" @add-history="addHistory" />
          </v-col>
          <v-col cols="5">
            <History :calculators="['Calculator A', 'Calculator B']" :history="history" @clear-history="clearHistory"/>
          </v-col>
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import Calculator from './components/Calculator'
import History from './components/History'
export default {
  name: 'App',

  components: {
    Calculator,
    History,
  },
  beforeMount: function (){
    try {
      const savedHistory = localStorage.getItem('history')
      if (savedHistory !== null) this.$set(this, 'history', JSON.parse(savedHistory))
      else this.$set(this, 'history', [])
    } catch (e) {
      this.$set(this, 'history', [])
    }
  },
  data: () => ({
    history: [],
  }),
  methods: {
    addHistory: function(item) {
      this.history = [item, ...this.history]
      localStorage.setItem('history', JSON.stringify(this.history))
    },
    clearHistory: function() {
      this.history = []
      localStorage.removeItem('history')
    }
  }
};
</script>
