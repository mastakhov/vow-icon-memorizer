<template>
  <div class="hello">
    <img :src="src">
  </div>
</template>

<script>
export default {
  name: 'vowImage',
  props: {
    src: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
