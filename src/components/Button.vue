<template>
  <div
    v-bind:style="{
      width: width,
      height: `${height*64 + (height-1)*4}px`,
      backgroundColor: '#1976d2',
      borderRadius: '10px',
      lineHeight: `${height*64 + (height-1)*4}px`,
      fontSize: '24px',
      color: 'white',
      boxShadow: '0 3px 1px -2px rgba(0,0,0,.2),0 2px 2px 0 rgba(0,0,0,.14),0 1px 5px 0 rgba(0,0,0,.12)',
      cursor: 'pointer',
    }"
  >
    {{symbol}}
  </div>
</template>

<script>
  export default {
    name: 'Button',
    props: {
      symbol: {},
      width: {
        type: String,
        default: '100%',
      },
      height: {
        type: Number,
        default: 1,
      },
    }
  }
</script>
