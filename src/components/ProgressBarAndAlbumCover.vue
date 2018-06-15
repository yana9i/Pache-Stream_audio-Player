<template>
    <div ref="root" >
      <div class="IProgressContainer">
        <div class="IIProgressContainer progress-transition" :style="{width:progress+'%'}">
            <div id="progress" >
            </div>
            <transition name="fade">
              <svg xmlns="http://www.w3.org/2000/svg" version="1.1" v-if="isPlaying" @click="$emit('toggle',isPlaying)">
                <polygon points="0,10 0,0 10,5"/>
              </svg>
            </transition>
        </div>
      </div>
        <div id="imgList">
          <div id="imgHolder" :class="isPlaying&&this.timer.remaining>3?'img-holder-playing':'img-holder-not-playing'" @click="$emit('toggle',isPlaying)">
            <img :src="recentSongs.nowPlay.song.art" id="nowPlayImg">
          </div>
        </div>
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
    }
  },
  data:function(){
    return{
      imgHolderStyle:{
        width:0,
      }
    }
  },
  mounted:function(){
    this.imgHolderStyle.width = this.$refs.root.offsetWidth
  }
};

</script>

<style scoped>
div.IProgressContainer{
  background-color: gray;
  border-radius: 10px;
  box-shadow: 0px 2px 4px 0px black;
}
div.IIProgressContainer {
  background-color: #fff;
  height: 3px;
  line-height: 10px;
  margin-top: 10px;
}
div.progress-transition {
  transition: width 1010ms linear;
}
div#progress {
  background-color: black;
  height: 3px;
  width: 100%;
}
svg {
  color: black;
  float: right;
  width: 10px;
  height: 10px;
  margin: -6px;
  z-index: -1;
  transform: scale(0.85)
}

div#imgList{
  display: flex;
  justify-content: center;
  align-items: center;
  overflow: hidden;
  height: 30vw;
  z-index: -3;
}
div#imgHolder{
  transition: all .8s;
  border-radius: 50%;
  width: 20vw;
  height: 20vw;
}
img {
  width: 20vw;
  height: 20vw;
  transition: all .8s;
  border-radius: 50%;
  z-index: -3;
}

.fade-enter-active, .fade-leave-active {
  transition: all .8s;
}
.fade-enter {
  opacity: 0;
  transform: translateX(-3px);
}
.fade-enter-to{
  opacity: 1;
}
.fade-leave {
  opacity: 1;
}
.fade-leave-to {
 opacity: 0;
 transform: translateX(3px);
}

div.img-holder-playing{
  transform: translate(0vw,-8vw);
}
div.img-holder-not-playing{
  transform: translate(0vw,0vw);
  box-shadow: 0px 2px 7px 0px black;
}
</style>

