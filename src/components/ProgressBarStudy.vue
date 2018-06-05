<template>
    <div class="progressContainer">  
     <div class="progress" :style="{width:progress+'%'}">  
          <b v-bind:style="{position:'absolute',left:progress/2+'%'}"></b>  
     </div>  
</div>  
</template>

<script>
export default {
    props:['progress']
}
</script>

<style>

 
div.progressContainer{  
          height: 10px;  
          width: 50%;  
          background-color: #ddd;  
          margin-left: 2%;  
}  
div.progress{  
            background-color: #1C8DE0;
            height:10px;  
            line-height: 10px; 
            transition: width 1000ms; 
}  
b{  
            color:#fff;  
            font-weight: 100;  
            font-size: 12px;  
            margin-left: 2%; 
              /* position:absolute;  
          left:40%;    */
 }  
</style>

