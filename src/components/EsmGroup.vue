<template>
  <div class="esm-group">
    <div v-for="(input, index) of inputs" :key="input.uuid" class="input">
      <esm v-model="inputs[index].data"/>
      <button @click="remove(index)" class="input-list-button danger">&times;</button>
    </div>
    <button @click="add()" class="input-list-button">+</button>
  </div>

</template>

<script>
import { v4 as uuidv4 } from 'uuid'
import Esm from './Esm.vue'

export default {
  data () {
    return {
      inputs: []
    }
  },
  methods: {
    add () {
      this.inputs.push({ uuid: uuidv4(), data: {} })
    },
    remove (index) {
      this.inputs.splice(index, 1)
    }
  },
  watch: {
    inputs () {
      this.$emit('input', this.inputs)
    }
  },
  name: 'EsmGroup',
  components: { Esm }
}
</script>

<style scoped>
.input-group {
  padding-left: 10px;
  display: flex;
  flex-direction: column;
  align-items: baseline;
  width: 100%;
}

.input {
  padding: 5px 0;
  display: flex;
  width: 100%;
  align-items: flex-start;
}

.input input {
  flex-grow: 1;
}

.input-list-button {
  font-size: 18px;
  color: gray;
  background: none;
  border: none;
  outline: none;
}

.input-list-button:hover {
  color: black;
  cursor: pointer;
}

.input-list-button.danger:hover {
  color: maroon;
}
</style>
