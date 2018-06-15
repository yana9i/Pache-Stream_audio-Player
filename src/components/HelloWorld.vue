<template>
  <div class="hello">
    <player-rec scr='http://10.18.3.111/api/nowplaying'></player-rec>
  </div>
</template>

<script>
import Player from './PlayerRec'

export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  },
  components:{
    'player-rec':Player
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #990307;
}
</style>
