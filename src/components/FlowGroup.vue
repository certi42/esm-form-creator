<template>
  <div class="flow-group">
    <div v-for="(input, index) of inputs" :key="input.uuid" class="input">
      <div style="display: flex; flex-direction: column;">
        <label>User Input: <input type="text" v-model="inputs[index].data.user_answer"></label>
        <label>ESMs: </label>
        <Esm v-model="inputs[index].data.next_esm.esm" :line="false"/>
      </div>
      <button @click="remove(index)" class="input-list-button danger">&times;</button>
    </div>
    <button @click="add()" class="input-list-button">+</button>
  </div>

</template>

<script>
import { v4 as uuidv4 } from 'uuid'

export default {
  data () {
    return {
      inputs: []
    }
  },
  methods: {
    add () {
      this.inputs.push({ uuid: uuidv4(), data: { user_answer: '', next_esm: { esm: {} } } })
    },
    remove (index) {
      this.inputs.splice(index, 1)
    }
  },
  watch: {
    inputs: {
      deep: true,
      handler () {
        this.$emit('input', this.inputs.map((input) => input.data))
      }
    }
  },
  beforeCreate: function () {
    // lazy load the `Esm` component because it's recursive.
    // ie. component tree looks like this:
    // <Esm>
    //   <FlowGroup>
    //     <Esm>
    //     ...

    this.$options.components.Esm = require('./Esm.vue').default
  },
  name: 'FlowGroup'
}
</script>

<style scoped>
.flow-group {
  display: flex;
  flex-direction: row;
}

.input {
  padding: 5px 0;
  display: flex;
  width: 100%;
  align-items: flex-start;
  justify-content: space-between;
  padding-left: 20px;
  border-left: 1px solid #999;
  border-image: linear-gradient(to bottom, #0000 0%, #888 10%, #888 90%, #0000 100%) 1 100%;
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
  width: min-content;
}

.input-list-button:hover {
  color: black;
  cursor: pointer;
}

.input-list-button.danger:hover {
  color: maroon;
}
</style>
