<template>
  <div class="componentheader">
    <h1>Component header</h1>
    <ul v-for="(mail, index) in arrayMail" :key="index">
      <li> {{ mail }}</li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'ComponentHeader',
  props:{
    arrayMail: {
      type: Array
    }
  }
}
</script>

<style>
</style>