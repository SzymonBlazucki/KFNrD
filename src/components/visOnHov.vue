<template>
<div>
  <svg width="100" height="100">
  <circle cx="50" cy="50" r="40" id="mouse" :fill="start" :opacity="opa" v-on:mouseover="mouseover" v-on:mouseleave="mouseleave"/>
</svg>
<svg width="100" height="100">
  <circle cx="50" cy="50" r="40" id="mouse" :fill="filling" :opacity="opa" v-on:mouseover="mouseover" v-on:mouseleave="mouseleave"/>
</svg>
<br/>
<svg width="200" height="100" class="back">
  <path d="m0 50 l200 0" :stroke="startComp" stroke-width="10"/>
</svg>
<svg width="25" height="100" class="back">
  <rect width="25" height="100" rx="5" ry="5" fill="black" stroke-width='0' />
  <text x="2" y="54" fill="white">Op</text>
</svg>
<svg width="200" height="100" class="back">
  <path d="m0 50 l200 0" :stroke="abc" stroke-width="10"/>
</svg>

  
</div>
</template>

<script lang="ts">


function giveColor(arr){
const a = [];
  for (let i=0;i<arr.length;i++){
  a.push(arr[i]*255)
  }
  return ("rgb("+a[0]+","+a[1]+","+a[2]+")");
  }

export default  {
  components: {
  },
  props: {
    hover: Array,
    leftBeam: Array

  } ,
      

  data: function() {
      return{
      abc: giveColor(this.hover),
      filling: "#fff",
      opa: 0.3,
      start: "#fff",
      startComp: giveColor(this.leftBeam)
  }},
  methods: {
    mouseover: function(){
      this.start = this.startComp
      this.filling = this.abc
      this.opa = 1
    },    
    mouseleave: function(){
      this.opa = 0.1
    },
  }
}

</script>

<style>
#mouse {
    stroke:gray;
    stroke-width: 2; 
}
.back {
  background-color:#00ccff
}

</style>