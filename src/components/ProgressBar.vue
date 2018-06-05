<template>
    <div>
        <svg width="300" height="100" viewBox="0 0 400 100">
            <line x1="10" y1="10" x2="310" y2="10" fill="none" stroke-width="12" stroke-linecap="round" stroke="#666" />
            <line ref="progressBar" id="progress" x1="10" y1="10" x2="310" y2="10" fill="none" stroke-width="12" stroke="blue" stroke-linecap="round" stroke-dasharray="300" :stroke-dashoffset="setStrokeDashoffset" />
        </svg>
        <p ref='sss' title="abc">para</p>
    </div>
</template>

<script>

export default {
    name:'progressBar',
    props:{
        percent:{
            type:Number,
            required:true
        },
    },
    data:function(){
        return{
            val:300
        }
    },
    computed:{
        setStrokeDashoffset:function(){
            return this.val*(1-this.percent);
        }
    },
    updated:function(){
        this.val = this.$refs.progressBar.getAttribute('stroke-dasharray');     

    }
}
</script>
