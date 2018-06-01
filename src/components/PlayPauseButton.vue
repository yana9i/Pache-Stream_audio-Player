<template>
    <div>
        <audio ref="audio" preload="meta" src="https://demo.azuracast.com/radio/8000/radio.mp3?1527775630">不支持 audio</audio>
        <button @click="togger">button</button>
        <music-info></music-info>
    </div>
</template>

<script>
import MusicInfo from './MusicInfo.vue'

export default {
    name:'Player',
    data () {
        return {
            'url' :null,
        }
    },
    computed : {
        getPlayer: function(){
            return this.$refs.audio;
        }
    },
    methods :{
        play: function(){
            this.$refs.audio.src = this.url;
            var audio = this.$refs.audio;
            audio.load();
            audio.play();
        },
        pause : function(){
            var audio = this.$refs.audio;
            audio.src = ''
            audio.pause();
            this.status = false;
        },
        togger : function(){
            if (!this.$refs.audio.paused){
                this.pause();
            }
            else {
                this.play();
            }
        }
    },
    components:{
        'music-info':MusicInfo
    },
    mounted : function(){
        this.url = this.$refs.audio.src;
        console.log(this.url);
        
    }
}
</script>