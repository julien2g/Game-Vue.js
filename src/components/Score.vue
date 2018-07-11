<template>
  <div>
    {{score ? 'Your score ' + score : 'Press Enter'}}
  </div>
</template>

<script>
export default {
  name: 'Score',
  data: function () {
    return {
      score: 0
    }
  }
}
</script>

<style scoped>

</style>
