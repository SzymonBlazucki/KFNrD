<template>
<div>
  <br/>
  <h5> Initial Conditions </h5>
    <KetViewer :vector="start" :dark-mode="false"/> <br/>
  <h5> Operation </h5>
    <MatrixViewer :operator-raw="vis" :dark-mode="false"/> <br/>
  <h5> product vector </h5>
    <KetViewer :vector="end" :dark-mode="false"/> <br/>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import HelloWorld from './HelloWorld.vue';
import { Dimension, Vector, Cx, Gates, Operator } from "quantum-tensors";
import { KetViewer, MatrixViewer } from "bra-ket-vue";
const colorDim = new Dimension('color', 3, ['R','G','B']) 

function check (letter){
  if (letter == 'R') return 0;
  else if (letter == 'G') return 1;
  else if (letter == 'B') return 2;
}

function operation (givenVector, matrix){
  const emptyVector = [["R", Cx(0)], ["G", Cx(0)],['B', Cx(0)]]
  for (let i=0; i<matrix.length; i++){
  emptyVector[check(matrix[i][0])][1].re += givenVector[check(matrix[i][0])][1].re*matrix[i][2].re
  }
  return emptyVector
}

function vectorCreator (arr){
  return [["R", Cx(arr[0])], ["G", Cx(arr[1])],['B', Cx(arr[2])]] 
}


const matrix1 = [
  ['R', 'R', Cx(1)],
  ['G', 'G', Cx(1)],
];

const matrix2 = [
  ['R', 'R', Cx(1)],
  ['R', 'G', Cx(1)],
  ['R', 'B', Cx(1)]
];
const matrix3 = [
  ['G', 'G', Cx(1)],
  ['G', 'B', Cx(1)],
];

export default  {

  components: {
    KetViewer,
    MatrixViewer
  },
  props: {
    personName: Array,
    matr: String
  } ,
      

  data: function() {
      return{
      person: this.personName[2],
      mata: eval(this.matr),
      start: Vector.fromSparseCoordNames(
        vectorCreator(this.personName),
        [colorDim]),
      vis: Operator.fromSparseCoordNames(
        eval(this.matr), [colorDim]),
       end:  Vector.fromSparseCoordNames(
        operation( vectorCreator(this.personName), eval(this.matr)),
        [colorDim]),
  }},


}

</script>