<template>
    <div>
        <audio-component :listenUrl='playStatus.station.listen_url' v-if='playStatus.station' ref='audio' @LoadUp="setLoadUpTrue" @NotLoading="setLoadUpFalse"></audio-component>
        <play-control-component :recent-songs='recentSongs' :is-playing='isPlaying' :is-load-up='isLoadUp' v-if="recentSongs" @PlayUp="playUp" @toggle="togglePlayer"></play-control-component>
        <img :src='recentSongs.nextPlay.song.art' v-show="false">
    </div>
</template>

<script>
import AudioComponent from "./AudioComponent";
import PlayControlComponent from "./PlayControlComponent";

export default {
  components: {
    AudioComponent: AudioComponent,
    PlayControlComponent: PlayControlComponent
  },
  props: {
    scr: {
      default: ""
    }
  },
  data: function() {
    return {
      isPlaying: false,
      isLoadUp: false,
      playStatus: "",
      recentSongs: {
        nowPlay: {},
        nextPlay: {
          song: {}
        },
        beforePlay: {
          song: {}
        }
      }
    };
  },
  methods: {
    getPlayerStatus: async function() {
      if (this.playStatus.nowPlay) {
        this.playStatus.nowPlay = this.playStatus.nextPlay;
      }
      var get = await this.$ajax.get(this.scr);
      this.playStatus = get.data[0];
      this.recentSongs.nowPlay = this.playStatus.now_playing;
      this.recentSongs.nextPlay = this.playStatus.playing_next;
      this.recentSongs.beforePlay = this.playStatus.song_history[0].song;
      console.log(this.recentSongs);
    },
    togglePlayer: function(emitPlaying) {
      this.$refs.audio.toggle();
      this.isPlaying = !emitPlaying;
    },
    setLoadUpTrue() {
      this.isLoadUp = true;
      console.log(this.isLoadUp);
    },
    setLoadUpFalse() {
      this.isLoadUp = false;
      console.log(this.isLoadUp);
    },
    async playUp() {
      this.recentSongs.nowPlay.elapsed = 0;
      await this.getPlayerStatus();
    }
  },
  mounted: function() {
    this.getPlayerStatus();
    setInterval(this.getPlayerStatus, 14449);
  }
};
</script>

