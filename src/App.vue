<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
      <div class="d-flex align-center">
        Double Calculator
      </div>
    </v-app-bar>

    <v-main>
      <v-container>
        <v-row class="text-center">
          <v-col cols="3">
            <Calculator name="Calculator A" @add-history="addHistory" />
          </v-col>
          <v-col cols="3">
            <Calculator name="Calculator B" @add-history="addHistory" />
          </v-col>
          <v-col cols="5">
            {{history}}
          </v-col>
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import Calculator from './components/Calculator'

export default {
  name: 'App',

  components: {
    Calculator,
  },

  data: () => ({
    history: [],
  }),
  methods: {
    addHistory: function(item) {
      this.history = [item, ...this.history]
    },
  }
};
</script>
