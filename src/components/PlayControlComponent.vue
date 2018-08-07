<template>
    <div>
        <now-playing-information :now-play-info='recentSongs.nowPlay.song' :progress='PlayingTimer' v-if='recentSongs.nowPlay.song&&getPlayRate' ></now-playing-information>
        <progress-bar-and-album-cover :progress="getPlayRate*100" :recentSongs="recentSongs" v-if="recentSongs.nowPlay.song" :timer="PlayingTimer" :isPlaying="isPlaying" :isLoadUp="isLoadUp" @toggle="$emit('toggle',isPlaying)"></progress-bar-and-album-cover>
    </div>
</template>

<script>
import NowPlayingInformation from "./NowPlayingInformation";
import ProgressBarAndAlbumCover from "./ProgressBarAndAlbumCover";

export default {
  components: {
    NowPlayingInformation,
    ProgressBarAndAlbumCover
  },
  props: {
    recentSongs: {
      type: Object
    },
    isPlaying: {
      default: false
    },
    isLoadUp: {
      default: false
    }
  },
  data: function() {
    return {
      PlayingTimer: {
        remaining: this.recentSongs.nowPlay.remaining,
        elapsed: this.recentSongs.nowPlay.elapsed,
        duration: this.recentSongs.nowPlay.duration
      },
      nowID: this.recentSongs.nextPlay.song
    };
  },
  methods: {
    iterateTime: function() {
      this.PlayingTimer.elapsed++;
      this.PlayingTimer.remaining--;
      if (this.PlayingTimer.elapsed >= this.PlayingTimer.duration) {
        this.PlayingTimer.duration = this.recentSongs.nextPlay.duration;
        this.PlayingTimer.elapsed = 1;
        this.PlayingTimer.remaining = this.recentSongs.nextPlay.duration;
        this.recentSongs.nowPlay.song = this.recentSongs.nextPlay.song;
      }
    }
  },
  computed: {
    getPlayRate: function() {
      return this.PlayingTimer.elapsed / this.PlayingTimer.duration;
    }
  },
  watch: {
    "recentSongs.nowPlay.remaining": function() {
      this.PlayingTimer.remaining = this.recentSongs.nowPlay.remaining;
      this.PlayingTimer.elapsed = this.recentSongs.nowPlay.elapsed;
      this.PlayingTimer.duration = this.recentSongs.nowPlay.duration;
    }
  },
  mounted() {
    setInterval(this.iterateTime, 1000);
  }
};
</script>
