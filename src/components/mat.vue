<template>
<div>
  <br/>
  <h5> Initial Conditions </h5>
    <KetViewer :vector="start" :dark-mode="false"/> <br/>
  <h5> Operation </h5>
    <MatrixViewer :operator-raw="vis" :dark-mode="false"/> <br/>
  <h5> product vector </h5>
    <KetViewer :vector="end" :dark-mode="false"/> <br/>
    <visOnHov :hover="hov" :leftBeam="initial"/>
  </div>

</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import HelloWorld from './HelloWorld.vue';
import { Dimension, Vector, Cx, Gates, Operator } from "quantum-tensors";
import { KetViewer, MatrixViewer } from "bra-ket-vue";
import visOnHov from './visOnHov.vue';
const colorDim = new Dimension('color', 3, ['R','G','B']) 

function check (letter){
  if (letter == 'R') return 0;
  else if (letter == 'G') return 1;
  else if (letter == 'B') return 2;
}

function operation (givenVector, matrix){
  const emptyVector = [["R", Cx(0)], ["G", Cx(0)],['B', Cx(0)]]
  for (let i=0; i<matrix.length; i++){
  emptyVector[check(matrix[i][0])][1].re += givenVector[check(matrix[i][1])][1].re*matrix[i][2].re
  }
  return emptyVector
}

function rawNumbers (givenVector, matrix){
  const arr = [0,0,0]
  for (let i=0; i<matrix.length; i++){
  arr[check(matrix[i][0])] += givenVector[check(matrix[i][1])][1].re*matrix[i][2].re
  }
  return arr
}

function vectorCreator (arr){
  return [["R", Cx(arr[0])], ["G", Cx(arr[1])],['B', Cx(arr[2])]] 
}

export default  {

  components: {
    KetViewer,
    MatrixViewer,
    visOnHov
  },
  props: {
    initial: Array,
    matr: Array
  } ,
      

  data: function() {
      return{
      person: this.initial[2],
      mata: this.matr,
      start: Vector.fromSparseCoordNames(
        vectorCreator(this.initial),
        [colorDim]),
      vis: Operator.fromSparseCoordNames(
        this.matr, [colorDim]),
      end:  Vector.fromSparseCoordNames(
        operation( vectorCreator(this.initial), this.matr),
        [colorDim]),
      hov: rawNumbers( vectorCreator(this.initial), this.matr)
  }},


}

</script>