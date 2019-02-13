<template>
  <div>
    <div>
      <!-- <app-header></app-header> -->
      <app-regi ></app-regi>
    </div>
  </div>
</template>

<script>
// import header from './Header.vue'
import regiform from './restform.vue'
export default {
  name: 'HelloWorld',

  components: {
    // 'app-header': header,
    'app-regi': regiform
  }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>

</style>
