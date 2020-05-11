<template>
<footer>
 <p v-html="footer"></p>
</footer>
</template>

<script>
export default {
  data () {
    return {
      footer: '<p>All the information was taken from <a href="https://digimon.fandom.com/wiki/Digimon_Adventure"> digimon wiki </a></p>'
    }
  }
}
</script>

<style>
footer p{
  margin-top: 5%;
}
</style>
