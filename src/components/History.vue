<template>
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
      v-for="(item, index) in history"
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
    <div
      v-bind:style="{
        position: 'absolute',
        bottom: '30px',
        right: '30px',
        fontSize: '24px',
        color: 'white',
        backgroundColor: 'red',
        borderRadius: '10px',
        padding: '5px 15px',
        boxShadow: '0 3px 1px -2px rgba(0,0,0,.2),0 2px 2px 0 rgba(0,0,0,.14),0 1px 5px 0 rgba(0,0,0,.12)',
        cursor: 'pointer',
      }"
      v-on:click="clearHistory"
    >
      Clear
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
    }
  },
  methods: {
    clearHistory: function() {
      this.$emit('clear-history')
    },
  }
}
</script>