<template>
  <v-container
    v-bind:style="{
      boxShadow: '0px 3px 3px -2px rgba(0,0,0,0.2), 0px 3px 4px 0px rgba(0,0,0,0.14), 0px 1px 8px 0px rgba(0,0,0,0.12)',
      borderRadius: '20px',
      padding: '10px 20px 20px 20px',
    }"
  >
    <v-row class="mb-5">
      <div
        v-bind:style="{ height: '48px', fontSize: '48px'}"
      >{{resultValue}}</div>
    </v-row>
    <v-row
      v-bind:style="{ fontSize: '24px', height: '36px' }"
    >
      {{inputValue}}
    </v-row>
    <v-row justify="">
      <v-col cols="9">
        <v-row class="mb-1">
          <Button symbol="C" width="33%" @paddle-click="clearValue"/>
          <Button symbol="x" value="*" width="33%" @paddle-click="paddleClick"/>
          <Button symbol="-" width="33%" @paddle-click="paddleClick"/>
        </v-row>
        <v-row class="mb-1">
          <Button symbol="7" width="33%" @paddle-click="paddleClick"/>
          <Button symbol="8" width="33%" @paddle-click="paddleClick"/>
          <Button symbol="9" width="33%" @paddle-click="paddleClick"/>
        </v-row>
        <v-row class="mb-1">
          <Button symbol="4" width="33%" @paddle-click="paddleClick"/>
          <Button symbol="5" width="33%" @paddle-click="paddleClick"/>
          <Button symbol="6" width="33%" @paddle-click="paddleClick"/>
        </v-row>
        <v-row class="mb-1">
          <Button symbol="1" width="33%" @paddle-click="paddleClick"/>
          <Button symbol="2" width="33%" @paddle-click="paddleClick"/>
          <Button symbol="3" width="33%" @paddle-click="paddleClick"/>
        </v-row>
        <v-row>
          <Button symbol="0" width="66%" @paddle-click="paddleClick"/>
          <Button symbol="." width="33%" @paddle-click="paddleClick"/>
        </v-row>
      </v-col>
      <v-col cols="3">
        <v-row>
          <Button symbol="+" height="2" class="mb-1" @paddle-click="paddleClick"/>
        </v-row>
        <v-row>
          <Button symbol="=" height="3" @paddle-click="submitValue"/>
        </v-row>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import Axios from 'axios'
import moment from 'moment'
import Button from './Button'
export default {
  name: 'Calculator',
  components: {
    Button,
  },
  props: {
    name: {
      type: String,
      default: 'Calculator'
    }
  },
  data: () => ({
    resultValue: '',
    inputValue: '',
    newRound: false,
  }),
  methods: {
    paddleClick: function(value) {
      if (this.newRound) {
        this.inputValue = value
        this.resultValue = ''
        this.newRound = false
      } else {
        this.inputValue += value
      }
    },
    submitValue: async function() {
      const formatedInput = encodeURIComponent(this.inputValue.replace('x','*')) 
      const res = await Axios.get(`http://api.mathjs.org/v4/?expr=${formatedInput}`)
      if (res && res.status === 200) {
        this.resultValue = res.data
      } else {
        this.resultValue = 'ERROR'
      }
      
      this.$emit('add-history', {
        result: this.resultValue,
        input: this.inputValue,
        time: `${moment().format('DD/MM/YYYY - HH:mm:ss')}`,
        name: this.name,
      })
      this.newRound = true
    },
    clearValue: function() {
      this.resultValue = ''
      this.inputValue = ''
      this.newRound = true
    }
  }
}
</script>
