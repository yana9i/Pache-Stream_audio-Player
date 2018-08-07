<template>
  <div class="hello">
    <player-rec scr='http://118.25.103.151/api/nowplaying'></player-rec>
    <link rel="shortcut icon" href="./static/favicon.ico">
  </div>
</template>

<script>
import Player from "./PacheStream-audioPlayer";

export default {
  name: "HelloWorld",
  data() {
    return {
      msg: "Welcome to Your Vue.js App"
    };
  },
  components: {
    "player-rec": Player
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1,
h2 {
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
