<template>
  <Monstera />
  <Variegata />
</template>

<script>
import Monstera from './components/Monstera.vue'
import Variegata from './components/Variegata.vue'

export default {
  name: 'App',
  components: { Monstera, Variegata }
}
</script>

<style>
body
{
  margin: 0px;
  color: rgb(219, 219, 211);
}
#app
{
  overflow: hidden;
}
</style>
