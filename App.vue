<template>
  <div id="app">
    {{title}}<br/>
    description - to be done later
    <!--<img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js + TypeScript App"/> -->
    <h2> Filtration</h2>
  <mat :initial="[1/3, 1/3, 1/3]" :matr='matrix1'> </mat>
    <h2> Fluorescence</h2>
  <mat :initial="[1/3, 1/3, 1/3]" :matr='matrix2'> </mat>
    <h2> Another type of the fluorescence</h2>
  <mat :initial="[1/3, 1/3, 1/3]" :matr='matrix3'> </mat>
  And now you can create your own operation. Just set up appropriate values in the input table and see what happens.
  <matrixCreator/> 

  <ball/>
  </div>

</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import HelloWorld from './components/HelloWorld.vue';
import { Dimension, Vector, Cx, Gates, Operator } from "quantum-tensors";
import { KetViewer, MatrixViewer } from "bra-ket-vue";
import mat from './components/mat.vue';
import matrixCreator from './components/matrixCreator.vue';

const colorDim = new Dimension('color', 3, ['R','G','B']) 
//mat: () => import('../components/mat.vue')
@Component({
  components: {
    HelloWorld,
    KetViewer,
    MatrixViewer,
    mat,
    matrixCreator,
  },
  data: function() {
    return {
      title: 'Project Matrix',
      matrix1: [
  ['R', 'R', Cx(1)],
  ['G', 'G', Cx(1)],
],
      matrix2: [
  ['R', 'R', Cx(1)],
  ['R', 'G', Cx(1)],
  ['R', 'B', Cx(1)]
],
       matrix3: [
  ['G', 'G', Cx(1)],
  ['G', 'B', Cx(1)],
],
      value: null
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
