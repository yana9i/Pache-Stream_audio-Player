<template>
    <div>
        <h1>Player component</h1>
        <player></player>
    </div>
</template>

<script>

import hw from "./HelloWorld.vue"
import player from "./PlayPauseButton"

export default {
    components:{
        'helloworld':hw,
        'player':player
    }
}
</script>

<style scoped>

</style>
