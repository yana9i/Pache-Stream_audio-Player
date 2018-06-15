<template>
    <div>
        <div>
            <transition mode="out-in"><div v-if='showTitle' key='real' id="title">{{nowPlayInfo.title}}</div></transition>
        </div>
        <div>
            <transition mode="out-in">
                <div v-if="showTitle" id="album-artist">
                    <transition mode="out-in">
                        <div v-if="carousel" key="album">{{nowPlayInfo.album}}</div>
                        <div v-else key="artist">{{nowPlayInfo.artist}}</div>
                    </transition>
                </div>
            </transition>
        </div>
    </div>
</template>

<script>
export default {
    props:{
        nowPlayInfo:{
            type:Object
        },
        progress:{
            type:Object
        }
    },
    data(){
        return{
            show:false,
            carousel:false
        }
    },
    computed:{
        showTitle:function(){
            return !(this.progress.remaining<3)
        }
    },
    created(){
        setInterval(()=>{this.carousel=!this.carousel},5000);
    }
}
</script>

<style scoped>
.v-enter-active, .v-leave-active {
    transition: opacity .5s;
}
.v-enter, .v-leave-to {
    opacity: 0;
}
.v-enter-to, .v-leave {
    opacity: 1;
}
div{
    text-align: center;
    color: #3A3A45
}
div#album-artist{
    font-weight: 100;
    white-space: nowrap;
    font-size: 0.6em;
    color: #999999;
}
div#title{
    font-weight: normal;
}
</style>
