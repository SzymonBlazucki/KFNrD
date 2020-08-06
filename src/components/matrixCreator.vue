<template>
<div>
   <table style="width:30%">
  <tr>
    <th> </th>
    <th>R</th>
    <th>G</th>
    <th>B</th>
  </tr>
  <tr>
    <td><b>R</b></td>
    <td><div class="box">
      <input v-model="value1" @input="clearErrorMsg" />
      <span style="color: red; margin-left: 20px;">{{ options.errorMsg }}</span>
    </div><vue-slider
      v-model="value1"
      v-bind="options"
      :tooltip="options.errorMsg ? 'none' : 'always'"
      @error="error"
      @change="clearErrorMsg"
    ></vue-slider>
   </td> 
    <td><div class="box">
      <input v-model="value2" @input="clearErrorMsg" />
      <span style="color: red; margin-left: 20px;">{{ options.errorMsg }}</span>
    </div><vue-slider
      v-model="value2"
      v-bind="options"
      :tooltip="options.errorMsg ? 'none' : 'always'"
      @error="error"
      @change="clearErrorMsg"
    ></vue-slider></td>
    <td><div class="box">
      <input v-model="value3" @input="clearErrorMsg" />
      <span style="color: red; margin-left: 20px;">{{ options.errorMsg }}</span>
    </div><vue-slider
      v-model="value3"
      v-bind="options"
      :tooltip="options.errorMsg ? 'none' : 'always'"
      @error="error"
      @change="clearErrorMsg"
    ></vue-slider>
    </td>
  </tr>
  <tr>
    <td><b>G</b></td>
    <td><div class="box">
      <input v-model="value4" @input="clearErrorMsg" />
      <span style="color: red; margin-left: 20px;">{{ options.errorMsg }}</span>
    </div><vue-slider
      v-model="value4"
      v-bind="options"
      :tooltip="options.errorMsg ? 'none' : 'always'"
      @error="error"
      @change="clearErrorMsg"
    ></vue-slider>
    </td>
    <td><div class="box">
      <input v-model="value5" @input="clearErrorMsg" />
      <span style="color: red; margin-left: 20px;">{{ options.errorMsg }}</span>
    </div><vue-slider
      v-model="value5"
      v-bind="options"
      :tooltip="options.errorMsg ? 'none' : 'always'"
      @error="error"
      @change="clearErrorMsg"
    ></vue-slider></td>
    <td><div class="box">
      <input v-model="value6" @input="clearErrorMsg" />
      <span style="color: red; margin-left: 20px;">{{ options.errorMsg }}</span>
    </div><vue-slider
      v-model="value6"
      v-bind="options"
      :tooltip="options.errorMsg ? 'none' : 'always'"
      @error="error"
      @change="clearErrorMsg"
    ></vue-slider>
    </td>
  </tr>
  <tr>
    <td><b>B</b></td>
    <td><div class="box">
      <input v-model="value7" @input="clearErrorMsg" />
      <span style="color: red; margin-left: 20px;">{{ options.errorMsg }}</span>
    </div><vue-slider
      v-model="value7"
      v-bind="options"
      :tooltip="options.errorMsg ? 'none' : 'always'"
      @error="error"
      @change="clearErrorMsg"
    ></vue-slider>
    </td>
    <td><div class="box">
      <input v-model="value8" @input="clearErrorMsg" />
      <span style="color: red; margin-left: 20px;">{{ options.errorMsg }}</span>
    </div><vue-slider
      v-model="value8"
      v-bind="options"
      :tooltip="options.errorMsg ? 'none' : 'always'"
      @error="error"
      @change="clearErrorMsg"
    ></vue-slider></td>
    <td><div class="box">
      <input v-model="value9" @input="clearErrorMsg" />
      <span style="color: red; margin-left: 20px;">{{ options.errorMsg }}</span>
    </div><vue-slider
      v-model="value9"
      v-bind="options"
      :tooltip="options.errorMsg ? 'none' : 'always'"
      @error="error"
      @change="clearErrorMsg"
    ></vue-slider>
    </td>
    
  </tr>
</table>
<button @click='button = 1'>Compute</button>
<button @click='button = 0'>Reset</button>
    <span v-if="button === 1">
  <mat :initial="[1/3, 1/3, 1/3]" :matr='createMatrix(value1, value2, value3, value4, value5, value6, value7, value8, value9)'></mat>
    </span >
  
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import HelloWorld from './HelloWorld.vue';
import { Dimension, Vector, Cx, Gates, Operator } from "quantum-tensors";
import { KetViewer, MatrixViewer } from "bra-ket-vue";
import mat from '../components/mat.vue';
import VueSlider from 'vue-slider-component'
import ERROR_TYPES from "vue-slider-component"
import 'vue-slider-component/theme/default.css'
const colorDim = new Dimension('color', 3, ['R','G','B']) 
const ERROR_TYPE = {
    VALUE: 1,
    INTERVAL: 2,
    MIN: 3,
    MAX: 4,
    ORDER: 5,}

export default  {

  components: {
      VueSlider,
      mat: () => import('../components/mat.vue')
  },
  props: {
    MatrixViewer
  } ,
      

  data: function() {
      return{
      value1: 1,
      value2: 1,
      value3: 1,
      value4: 1,
      value5: 1,
      value6: 1,
      value7: 1,
      value8: 1,
      value9: 1,
      options:{
        min: 0,
        max: 1,
        errorMsg: '',
        interval: 0.01,
        marks: [0, 1]
      },
      button: 0,
  }},
methods: {
      error(type, msg) {
        switch (type) {
          case ERROR_TYPE.MIN:
            break
          case ERROR_TYPE.MAX:
            break
          case ERROR_TYPE.VALUE:
            break
        }
        this.options.errorMsg = msg
      },
      clearErrorMsg() {
        this.options.errorMsg = ''
      },
      createMatrix(value1, value2, value3, value4, value5, value6, value7, value8, value9){
          return [
  ['R', 'R', Cx(value1)],
  ['R', 'G', Cx(value2)],
  ['R', 'B', Cx(value3)],
  ['G', 'R', Cx(value4)],
  ['G', 'G', Cx(value5)],
  ['G', 'B', Cx(value6)],
  ['B', 'R', Cx(value7)],
  ['B', 'G', Cx(value8)],
  ['B', 'B', Cx(value9)],
]
      },
      reload() {
          this.$forceUpdate();
      },
      again() {
        this.button = 0;
        this.button = 1;
      }
    }
    

}

</script>