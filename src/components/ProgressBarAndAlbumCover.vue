<template>
    <div ref="root" id="root">
      <div class="IProgressContainer">
        <div class="IIProgressContainer progress-transition" :style="{width:progress+'%'}">
            <div id="progress" >
            </div>
            <transition name="fade-x">
              <div @click="$emit('toggle',isPlaying)" v-if="!isPlaying">
                <svg xmlns="http://www.w3.org/2000/svg" version="1.1" >
                  <polygon points="0,10 0,0 8.660254037844386,5"/>
                </svg>
              </div>
            </transition>
            <transition name="fade-y">
              <div  @click="$emit('toggle',isPlaying)" v-if="isPlaying">
                <svg xmlns="http://www.w3.org/2000/svg" version="1.1" style="transform:translate(-1px,-6px)">
                  <polygon points="10,0 0,0 5,8.660254037844386"/>
                </svg>
              </div>
            </transition>
        </div>
      </div>
        <div id="imgList" >
            <div id="outerLine">
              <transition name="fade2">
                <template  v-if="!isPlaying&&timer.remaining>3">
                  <div id="outerLine1">
                    <div id="outerLine2">
                    </div>
                  </div>
                </template>
              </transition>
              <transition name="fade2" mode="out-in">
                <div v-if='timer.remaining>1.5' >
                    <div id="imgHolder" :class="isPlaying&&(timer.remaining>3)?'img-holder-playing':'img-holder-not-playing'" @click="$emit('toggle',isPlaying)">
                      <img :src="recentSongs.nowPlay.song.art" id="nowPlayImg" :style="coverAni,{transform:'rotate('+imgRotate+'deg)'}" >
                    </div>
                </div>
              </transition>
            </div>
        </div>
        <img :src="recentSongs.nextPlay.song.art" v-show="false">
    </div>
</template>

<script>
export default {
  props: {
    progress:{
      type:Number,
      default:10
    },
    recentSongs:{
      type:Object
    },
    timer:{
      type:Object
    },
    isPlaying:{
      type:Boolean,
      default:false
    },
    isLoadUp:{
      type:Boolean,
      default:false
    }
  },
  data:function(){
    return{
      coverAni:{
        transitionProperty:'all',
        transitionDuration:'0s',
        transitionTimingFunction:'linear'
      },
      imgRotate:0,
      intervalId:null,
    }
  },
  watch:{
    isLoadUp:function(){
      if(this.isLoadUp&&this.timer.remaining>3){
        console.log(this.isLoadUp);
        this.transitionDuration='1s';
        this.transitionTimingFunction='linear';
        this.intervalId = setInterval(()=>{this.imgRotate+=5},100);
      }
      else{
        clearInterval(this.intervalId);
        this.transitionTimingFunction='ease';
        var closedRotate = this.imgRotate % 360;
        if(closedRotate < 180 )
          this.imgRotate-=closedRotate;
        else
          this.imgRotate=this.imgRotate-closedRotate+360;
      }
    }
  }
};

</script>

<style scoped>
div#root{
  z-index: -10;
}
div.IProgressContainer{
  background-color: #999;
  border-radius: 10px;
  box-shadow: 0px 1px 3px 0px #999;
  margin-top: 10px;
}
div.IIProgressContainer {
  height: 3px;
  line-height: 10px;
  align-items: center;
  justify-content: center;
}
div.progress-transition {
  transition: width 1010ms linear;
}
div#progress {
  background-color: #3a3a45;
  height: 2px;
  width: 100%;
}
svg {
  color: black;
  float: right;
  width: 10px;
  height: 10px;
  margin: -6px;
  z-index: -1;
  transform: scale(1.1);
  cursor: pointer;
}

div#imgList{
  display: flex;
  justify-content: center;
  align-items: center;
  overflow: hidden;
  height: 60vh;
  z-index: -10;
}
div#imgHolder{
  transition: all .8s;
  border-radius: 50%;
  width: 20vw;
  height: 20vw;
  z-index: 1999;
  cursor: pointer;
}
img {
  width: 20vw;
  height: 20vw;
  transition: all .8s;
  border-radius: 50%;
  z-index: -3;
}

img#img-transition {
  opacity: 0;
}
img#img-not-transition {
  opacity: 1;
}

.fade-x-enter-active, .fade-x-leave-active {
  transition: all .8s;
}
.fade-x-enter {
  opacity: 0;
  transform: translateX(-50px);
}
.fade-x-enter-to{
  opacity: 1;
}
.fade-x-leave {
  opacity: 1;
}
.fade-x-leave-to {
 opacity: 0;
 transform: translateX(50px);
}

.fade-y-enter-active, .fade-y-leave-active {
  transition: all .6s;
}
.fade-y-enter, .fade-y-leave-to {
  opacity: 0;
  transform: translateY(-3px);
}
.fade-y-enter-to{
  opacity: 1;
}
.fade-y-leave {
  opacity: 1;
}

div.img-holder-playing{
  transform: translate(0vw,-30vh);
}
div.img-holder-not-playing{
  transform: translate(0vw,0vw);
  box-shadow: 0px 2px 7px 0px #999;
}

.fade2-enter-active, .fade2-leave-active {
  transition: all .5s;
}
.fade2-enter {
  opacity: 0;
}
.fade2-enter-to{
  opacity: 1;
}
.fade2-leave {
  opacity: 1;
}
.fade2-leave-to {
 opacity: 0;
}

div#outerLine2 {
  position: absolute;
  border:1px solid;
  width: 20vw;
  height: 20vw;
  border-radius: 50%;
  border-color:#3a3a45;
  transform: translate(-1px,-1px) scale(1.01);
  animation:outerLineAni 2.5s ease 0.6s infinite;
}

@keyframes outerLineAni {
  0% {
    transform:translate(-1px,-1px) scale(1);
    opacity: 0;
  }
  30% {
    transform:translate(-1px,-1px) scale(1.12);
    opacity: 1;
  }
  750% {
    transform:translate(-1px,-1px) scale(1.17);
    opacity: 1;
  }
  100% {
    transform:translate(-1px,-1px) scale(1.25);
    opacity: 0;
  }
}
</style>

