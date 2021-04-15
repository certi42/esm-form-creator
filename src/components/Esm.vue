<template>
  <div class="esm">
    <select v-model.number="inputType">
      <option value=1>Text</option>
      <option value=2>Radio</option>
      <option value=3>Checkbox</option>
      <option value=4>Likert</option>
      <option value=5>Quick Answer</option>
      <option value=6>Slider</option>
      <option value=7>Date Time</option>
      <option value=8>PAM</option>
      <option value=9>Number</option>
      <option value=10>Web</option>
      <option value=11>Date</option>
      <option value=12>Time</option>
      <option value=13>Clock</option>
      <option value=14>Picture</option>
      <option value=15>Audio</option>
      <option value=16>Video</option>
    </select>
    <div class="input">
      <div v-if="inputType == 2">
        <!-- Radio -->
        <label>Radio: <input-group type="text" v-model="data.radios"/></label>
      </div>
      <div v-else-if="inputType == 3">
        <!-- Checkbox -->
        <label>Checkbox: <input-group type="text" v-model="data.checkboxes"/></label>
      </div>
      <div v-else-if="inputType == 4">
        <!-- Likert -->
        <label>Max: <input type="number" v-model.number="data.likert_max"></label>
        <label>Max Label: <input type="text" v-model="data.likert_max_label"></label>
        <label>Min Label: <input type="text" v-model="data.likert_min_label"></label>
        <label>Step: <input type="number" v-model.number="data.likert_step"></label>
      </div>
      <div v-else-if="inputType == 5">
        <!-- Quick Answer -->
        <label>Quick Answer: <input-group type="text" v-model="data.quick_answers"/></label>
      </div>
      <div v-else-if="inputType == 6">
        <!-- Slider -->
        <label> Min: <input type="number" v-model.number="data.scale_min"></label>
        <label>Max: <input type="number" v-model.number="data.scale_max"></label>
        <label>Start: <input type="number" v-model.number="data.scale_start"></label>
        <label>Max Label: <input type="text" v-model="data.scale_max_label"></label>
        <label>Min Label: <input type="text" v-model="data.scale_min_label"></label>
        <label>Step: <input type="number" v-model.number="data.scale_step"></label>
      </div>
      <div v-else-if="inputType == 10">
        <!-- Web -->
        <label>URL: <input type="url" v-model="data.url"></label>
      </div>
      <div v-else-if="inputType == 14 || inputType == 16">
        <!-- Picture -->
        <label>Camera: <input type="number" v-model.number="data.camera"></label>
      </div>
      <div>
        <label>Title: <input type="text" v-model="data.title"></label>
        <label>Instructions: <input type="text" v-model="data.instructions"></label>
        <label>Submit: <input type="text" v-model="data.submit"></label>
        <label>Expiration Threshold: <input type="number" v-model.number="data.expiration_threshold"></label>
        <div style="margin: 5px">Flows: <flow-group v-model="data.flows"/></div>
      </div>
    </div>
  </div>
</template>

<script>
import FlowGroup from './FlowGroup.vue'
import InputGroup from './InputGroup.vue'
export default {
  data () {
    return {
      inputType: 1,
      data: {}
    }
  },
  methods: {
    updateInputs () {
      if (this.inputType === 2) {
        this.data = { radios: ['YES', 'NO'] }
      } else if (this.inputType === 3) {
        this.data = { checkboxes: ['One', 'Two', 'Other'] }
      } else if (this.inputType === 4) {
        this.data = {
          likert_max: 5,
          likert_max_label: 'Good',
          likert_min_label: 'Bad',
          likert_step: 1
        }
      } else if (this.inputType === 5) {
        this.data = { quick_answers: ['Yes', 'No', 'Maybe'] }
      } else if (this.inputType === 6) {
        this.data = {
          scale_min: 0,
          scale_max: 10,
          scale_start: 5,
          scale_max_label: '10',
          scale_min_label: '0',
          scale_step: 1
        }
      } else if (this.inputType === 10) {
        this.data = { url: 'https://xxxx.xxxx.xxxx' }
      } else if (this.inputType === 14 || this.inputType === 16) {
        this.data = { camera: 0 }
      } else {
        this.data = {}
      }
      this.data = {
        ...this.data,
        type: this.inputType,
        title: 'EDIT HERE',
        instructions: 'EDIT HERE',
        submit: 'Submit',
        expiration_threshold: 60,
        flows: []
      }
    }
  },
  mounted () {
    this.$watch('data', () => this.$emit('input', this.data), { deep: true })
    this.updateInputs()
  },
  watch: {
    inputType () {
      this.updateInputs()
    }
  },
  components: { InputGroup, FlowGroup },
  props: ['value'],
  emits: ['input'],
  name: 'Esm'
}
</script>

<style scoped>
.esm select {
  margin: 5px;
}
.input {
  padding: 5px 0;
  display: flex;
  width: 100%;
  align-items: flex-start;
}

.input div {
  display: flex;
  flex-direction: column;
}

.input div label {
  display: flex;
  margin: 5px;
}

.input div label input {
  margin-left: 10px;
  flex-grow: 1;
}
</style>
