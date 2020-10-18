<template>
  <div>
    <v-row
      class="flex-row align-center"
      v-bind:style="{
        padding: '20px',
      }">
      <div
        v-bind:style="{
          fontSize: '24px'
        }"
      >Results</div>
      <v-text-field
        v-model="textSearch"
        outlined
        label="Search by results, date"
        v-bind:style="{
          height: '56px',
          maxHeight: '56px',
          marginRight: '10px',
          marginLeft: '10px',
          width: '60%',
        }"
      />
      <v-select
        v-model="nameSearch"
        outlined
        :items="calculatorNameOptions"
        label="Calculator"
        v-bind:style="{
          height: '56px',
          maxHeight: '56px',
          width: '20%',
        }"
      />

    </v-row>
    <div
      v-bind:style="{
        boxShadow: '0px 3px 3px -2px rgba(0,0,0,0.2), 0px 3px 4px 0px rgba(0,0,0,0.14), 0px 1px 8px 0px rgba(0,0,0,0.12)',
        borderRadius: '20px',
        padding: '10px 20px 20px 20px',
        height: '650px',
        overflow: 'scroll',
        position: 'relative',
      }">
      <div
        v-for="(item, index) in filterdHistory"
        :key="index"
        v-bind:style="{
          padding: '20px',
        }"
      >
        <v-row class="justify-space-between">
          <div v-bind:style="{ fontSize: '24px' }">{{item.name}}</div>
          <div v-bind:style="{ fontSize: '24px', color: '#1976d2', opacity: '0.6' }">{{item.time}}</div>
        </v-row>
        <v-row v-bind:style="{ fontSize: '48px', borderBottom: '1px solid #bbb' }">
          {{item.result}}
        </v-row>
        <v-row v-bind:style="{ fontSize: '24px' }">
          {{item.input}}
        </v-row>
      </div>
      <v-btn
          color="red"
          dark
          v-on:click="clearHistory"
          v-bind:style="{
            position: 'absolute',
            bottom: '30px',
            right: '30px',
          }"
        >
          Clear
        </v-btn>

      <v-dialog
        v-model="confirm"
        width="500"
      >
        <v-card>
          <v-card-title class="headline grey lighten-2">
            Are you sure?
          </v-card-title>
          <v-card-text>
            Calculator history will be deleted forever and can not restore.
          </v-card-text>
          <v-divider></v-divider>
          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn
              color="primary"
              text
              v-on:click="confirmClearHistory"
            >
              OK
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>
    </div>
  </div>
</template>
<script>
export default {
  name: 'History',
  props: {
    history: {
      type: Array,
      default: () => [],
    },
    calculators: {
      type: Array,
      default: () => ['All'],
    }
  },
  data: function() {
    return {
      textSearch: '',
      nameSearch: 'All',
      confirm: false,
    }
  },
  computed: {
    calculatorNameOptions: function() {
      return ['All', ...this.calculators]
    },
    filterdHistory: function () {
      return this.history.filter((item) => {
        const resultString = item.result + ''
        return this.textSearch === ''
        || resultString.indexOf(this.textSearch) >= 0
        || item.time.indexOf(this.textSearch) >= 0
      })
      .filter((item) => {
        return this.nameSearch == 'All'
        || item.name === this.nameSearch
      })
    }
  },
  methods: {
    clearHistory: function() {
      this.confirm = true
    },
    confirmClearHistory: function() {
      this.confirm = false
      this.$emit('clear-history')
    }
  }
}
</script>