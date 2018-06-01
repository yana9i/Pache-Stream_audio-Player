<template>
    <div>
        <h2>ID : {{nowPlaying.id}}</h2>
        <h2>Title : {{nowPlaying.title}}</h2>
        <h2>Artis : {{nowPlaying.artist}}</h2>
        <h2>Album : {{nowPlaying.album}}</h2>
        <p>{{playTime.elapsed}}+{{playTime.remaining}}={{playTime.duration}}</p>
        <p>{{this.computePercent}}</p>
    </div>
</template>
对象
<script>
var nextMusic={
}

export default {
    name:'musicinfo',
    data: function(){
        return {
            playTime:{
                duration:0,
                elapsed:0,
                remaining:999
            },
            nowPlaying:{
                'id':null,
                'artist':"Artist",
                'title':"Title",
                'album':"Album",
                'art':''
            }
        }
    },
    methods:{
        //取得正在播放音乐数据
        getNowPlaying:async function(){
            var nowplaying =  await this.$ajax.get('https://demo.azuracast.com/api/nowplaying')
            nextMusic = nowplaying.data[0].playing_next;
            nowplaying = nowplaying.data[0].now_playing;
            this.playTime.elapsed = nowplaying.elapsed;
            this.playTime.duration = nowplaying.duration;
            this.playTime.remaining = nowplaying.remaining;
            nowplaying = nowplaying.song;
            this.nowPlaying.id = nowplaying.id;
            this.nowPlaying.artist = nowplaying.artist;
            this.nowPlaying.title = nowplaying.title;
            this.nowPlaying.album = nowplaying.album;
        },
        //已播未播时间递增递减并更新正在播放信息
        iterateTimer:function(){
            this.playTime.remaining--;
            this.playTime.elapsed++;
            if(this.playTime.elapsed>=this.playTime.duration){
                this.playTime.elapsed = this.playTime.duration;
                this.playTime.remaining = 0;
                this.nowPlaying.id = nextMusic.id;
                this.nowPlaying.title = nextMusic.title;
                this.nowPlaying.artist = nextMusic.artist;
                this.nowPlaying.album = nextMusic.album;
                this.getNowPlaying();
            }
        }
    },
    computed:{
        computePercent:function(){
            return parseFloat(this.playTime.elapsed)/parseFloat(this.playTime.duration);
        }
    },
    mounted : function(){
        this.getNowPlaying();
        setInterval(this.iterateTimer,1000);
        setInterval(this.getNowPlaying,20000);
    }
}
</script>
