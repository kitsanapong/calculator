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
      <v-container>
        <v-row class="text-center">
          <v-col cols="3">
            <Calculator name="Calculator A" @add-history="addHistory" />
          </v-col>
          <v-col cols="3">
            <Calculator name="Calculator B" @add-history="addHistory" />
          </v-col>
          <v-col cols="5"
            v-bind:style="{
              boxShadow: '0px 3px 3px -2px rgba(0,0,0,0.2), 0px 3px 4px 0px rgba(0,0,0,0.14), 0px 1px 8px 0px rgba(0,0,0,0.12)',
              borderRadius: '20px',
              padding: '10px 20px 20px 20px',
            }"
          >
            <div v-for="(item, index) in history" :key="index">
              <v-row class="justify-space-between">
                <div>{{item.name}}</div>
                <div>{{item.time}}</div>
              </v-row>
              <v-row>
                {{item.result}}
              </v-row>
              <v-row>
                {{item.input}}
              </v-row>
            </div>
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
