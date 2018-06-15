<template>
    <div>
        <audio-component :listenUrl='playStatus.station.listen_url' v-if='playStatus.station' ref='audio' @toggle="togglePlayer"></audio-component>
        <play-control-component :recent-songs='recentSongs' :is-playing='isPlaying' v-if="recentSongs" @PlayUp="getPlayerStatus" @toggle="togglePlayer"></play-control-component>
    </div>
</template>

<script>
import AudioComponent from './AudioComponent'
import PlayControlComponent from './PlayControlComponent'

export default {
    components:{
        'AudioComponent':AudioComponent,
        'PlayControlComponent':PlayControlComponent
    },
    props:{
        scr:{
            default:''
        }
    },
    data:function(){
        return{
            isPlaying:false,
            playStatus:'',
            recentSongs:{
                nowPlay:{},
                nextPlay:{
                    song:{}
                },
                beforePlay:{
                    song:{}
                }
            }
        }
    },
    methods:{
        getPlayerStatus:async function(){
            var get =await this.$ajax.get(this.scr);
            this.playStatus = get.data[0];
            this.recentSongs.nowPlay = this.playStatus.now_playing;
            this.recentSongs.nextPlay = this.playStatus.playing_next;
            this.recentSongs.beforePlay = this.playStatus.song_history[0].song;
            console.log(this.recentSongs);
        },
        togglePlayer:function(emitPlaying){
            this.$refs.audio.toggle();
            this.isPlaying = !emitPlaying
        }
    },
    mounted:function(){
        this.getPlayerStatus();
        setInterval(this.getPlayerStatus,20000);    }
}
</script>

