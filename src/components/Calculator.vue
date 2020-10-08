<template>
  <v-container>
    <v-row>124</v-row>
    <v-row>2 x 62</v-row>
    <v-row justify="">
      <v-col cols="9">
        <v-row class="mb-1">
          <Button symbol="C"/>
          <Button symbol="x" class="mx-1"/>
          <Button symbol="-"/>
        </v-row>
        <v-row class="mb-1">
          <Button symbol="7"/>
          <Button symbol="8" class="mx-1"/>
          <Button symbol="9"/>
        </v-row>
        <v-row class="mb-1">
          <Button symbol="4"/>
          <Button symbol="5" class="mx-1"/>
          <Button symbol="6"/>
        </v-row>
        <v-row class="mb-1">
          <Button symbol="1"/>
          <Button symbol="2" class="mx-1"/>
          <Button symbol="3"/>
        </v-row>
        <v-row>
          <Button symbol="0" width="2" class="mr-1"/>
          <Button symbol="."/>
        </v-row>
      </v-col>
      <v-col cols="3">
        <v-row>
          <Button symbol="+" height="2" class="mb-1"/>
        </v-row>
        <v-row>
          <Button symbol="=" height="3"/>
        </v-row>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import Button from './Button'
export default {
  name: 'Calculator',
  components: {
    Button,
  },
  data: () => ({
    ecosystem: [
    ],
  }),
}
</script>
