<template>
  <div>
    <span v-html="welcomeMessage" :class="{ hide: !player }">{{ welcomeMessage }}</span>

    <form @submit.prevent="setPlayer" :class="{ hide: player }">
      <input name="player" placeholder="What's your name"  />
      <button type="submit">Play</button>
    </form>
  </div>
</template>

<script>
  export default {
    name: 'Player',
    data: function () {
      return {
        player: '',
        welcomeMessage: ''
      }
    },
    updated: function () {
      this.welcomeMessage = `Hello <span class="player"> ${ this.player }</span> !`
    },
    methods: {
      setPlayer: function (event) {
        let playerName = event.target[0].value
        if(!playerName) {
          window.alert('Please fill your name')
          return
        }
        this.player = playerName
      }
    },

  }
</script>

<style scoped>
.hide{
  display: none;
}
</style>
