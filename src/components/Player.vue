<template>
    <div>
        <h1>Player component</h1>
        <player-button></player-button>
        <music-info></music-info>
    </div>
</template>

<script>

import hw from "./HelloWorld.vue"
import playerPauseButton from "./PlayPauseButton"
import musicInfo from "./MusicInfo"
import ProgressBarStudy from "./ProgressBarStudy"

export default {
    components:{
        'helloworld':hw,
        'player-button':playerPauseButton,
        'music-info':musicInfo,
        'progress-bar-study':ProgressBarStudy
    }
}
</script>

<style scoped>

</style>
