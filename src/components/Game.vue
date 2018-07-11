<template>
  <div class="content">
  <div class="game" @click="clickOnInterface">
    <span class="round" :style="roundStyle" :class="{bonus: bonusActivated}" @click.stop="clickOnRound"
          @click.alt.stop="bonus"></span>
  </div>
  <div class="log">
<p v-for="item in collection">{{item}}</p>
  </div>
  </div>
</template>

<script>
  export default {
    name: 'Game',
    data: function () {
      return {
        click: 0,
        roundStyle: {
          width: '50px',
          height: '50px',
          margin: '20% 20%'
        },
        bonusActivated: false,
        collection: ['message 1', 'message 2']
      }
    },
    created: function () {
      document.onkeydown = this.start
    },
    watch: {
      click: function () {
        this.updateRound()
      }
    },
    methods: {
      clickOnRound: function (event) {
        this.click++
        this.collection.unshift(`Congrats ! (${this.click})`)
      },
      bonus: function (event) {
        if (this.bonusActivated)
        {
          this.click++
          this.collection.unshift(`Congrats x 2 ! (${this.click} + 2 )`)
        }
      },
      clickOnInterface: function (event) {
        this.click--
        this.collection.unshift(`太可惜了 ! (${this.click})`)
      },
      start: function (event) {
        if (event.key === 'Enter') {
          console.log('start')
        }
      },
      updateRound: function () {
        let size = Math.random() * (100 - 10) + 10
        let top = Math.random() * (60 - 5) + 5
        let left = Math.random() * (80 - 5) + 5

        this.bonusActivated = size > 80

        this.roundStyle.with = this.roundStyle.height = `${size}px`
        this.roundStyle.margin = `${top}% ${left}%`
      }
    }
  }
</script>

<style scoped>
  .content {
    height: 800px;
  }
  .game {
    width: 100%;
    height: 90%;
    display: block;
    background: darkslategrey;
  }
.log{
  width: 100%;
  height: 50px;
  background: #666;
  display: block;
  overflow: hidden;
}
  .round {
    width: 50px;
    height: 50px;
    background: aliceblue;
    border-radius: 9999px;
    position: absolute;
    margin: 20% 20%;
  }

  .bonus {
    background: red;
  }
</style>
