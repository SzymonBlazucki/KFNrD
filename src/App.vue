<template>
  <div id="app">
    {{title}}<br/>
    description - to be done later
    <!--<img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js + TypeScript App"/> -->
    <h2> Initial Conditions</h2>
    <KetViewer :vector="singlet" :dark-mode="false"/>
    <h2> Filtration</h2>
    <MatrixViewer :operator-raw="opfilter" :dark-mode="false"/>
    <KetViewer :vector="filter" :dark-mode="false"/>
    <h2> Fluorescence</h2>
    <MatrixViewer :operator-raw="opflu1" :dark-mode="false"/>
    <KetViewer :vector="flu1" :dark-mode="false"/>
    <h2> Another type of the fluorescence</h2>
    <MatrixViewer :operator-raw="opflu2" :dark-mode="false"/>
    <KetViewer :vector="flu2" :dark-mode="false"/>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import HelloWorld from './components/HelloWorld.vue';
import { Dimension, Vector, Cx, Gates, Operator } from "quantum-tensors";
import { KetViewer, MatrixViewer } from "bra-ket-vue";
const colorDim = new Dimension('color', 3, ['R','G','B']) 

function product(matrix, emptyVector = [["R", Cx(0)], ["G", Cx(0)],['B', Cx(0)]]){
  for (let i=0;i<matrix.length;i++){
    if (matrix[i][0] == "R") emptyVector[0][1].re += matrix[i][2].re;
    else if (matrix[i][0] == "G") emptyVector[1][1].re += matrix[i][2].re;
    else if (matrix[i][0] == "B") emptyVector[2][1].re += matrix[i][2].re;
  }
return emptyVector;
}

const case0 = [["R", Cx(1/3)], ["G", Cx(1/3)],['B', Cx(1/3)]];

const matrix1 = [
  ['R', 'R', Cx(1/3)],
  ['G', 'G', Cx(1/3)],
];
const matrix2 = [
  ['R', 'R', Cx(1/3)],
  ['R', 'G', Cx(1/3)],
  ['R', 'B', Cx(1/3)]
];
const matrix3 = [
  ['G', 'G', Cx(1/3)],
  ['G', 'B', Cx(1/3)],
];

const singlet = Vector.fromSparseCoordNames(
 case0,
  [colorDim]
);

const opfiltration = Operator.fromSparseCoordNames(
  matrix1, [colorDim]);

const filtration = Vector.fromSparseCoordNames(
 product(matrix1),
  [colorDim]
);
const opFluGkill = Operator.fromSparseCoordNames(
  matrix2, [colorDim]);

const FluGkill = Vector.fromSparseCoordNames(
 product(matrix2),
  [colorDim]
);

const opFluGkillR = Operator.fromSparseCoordNames(
  matrix3, [colorDim]);

const FluGkillR = Vector.fromSparseCoordNames(
 product(matrix3),
  [colorDim]
);

@Component({
  components: {
    HelloWorld,
    KetViewer,
    MatrixViewer
  },
  data: function() {
    return {
      singlet,
      filter: filtration,
      flu1: FluGkillR,
      flu2: FluGkill,
      opfilter: opfiltration,
      opflu1: opFluGkillR,
      opflu2: opFluGkill,
      title: 'Project Matrix',
    };
  },
  
})
export default class App extends Vue {}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
