<template>
    <div>
            <div>
                <audio ref="audio" preload="meta" :src="url">不支持 audio</audio>
            </div>
    </div>
</template>

<script>

export default {
    data () {
        return {
            'url' :null,
            'audio':null,
            'isPlaying':false
        }
    },
    props:{
        listenUrl:{
            default:''
        }
    },
    methods :{
        play: function(){
            this.audio.src = this.listenUrl;
            this.audio.load();
            this.audio.play();
            this.isPlaying = true;
        },
        pause : function(){
            this.audio.src = ''
            this.audio.pause();
            this.isPlaying = false;
        },
        toggle : function(){
            if (this.isPlaying){
                this.pause();
            }
            else {
                this.play();
            }
            console.log("Audio is playing:"+this.isPlaying);
        }
    },
    mounted : function(){
        this.audio = this.$refs.audio;
        this.audio.src = this.listenUrl;
        this.url = this.audio.src;
        this.isPlaying = false;       
    }
}
</script>

<style scoped>

</style>
