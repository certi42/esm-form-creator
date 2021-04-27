<template>
  <div class="input-group">
    <div v-for="(input, index) of inputs" :key="index" class="input">
      <input v-model="inputs[index]" :type="type"/>
      <button @click="remove(index)" class="input-list-button danger">&times;</button>
    </div>
    <button @click="add()" class="input-list-button">+</button>
  </div>
</template>

<script>
export default {
  data () {
    return {
      inputs: []
    }
  },
  methods: {
    add () {
      this.inputs.push('')
    },
    remove (index) {
      this.inputs.splice(index, 1)
    }
  },
  watch: {
    inputs () {
      if (this.type === 'number') {
        this.$emit('input', this.inputs.map(Number))
      } else {
        this.$emit('input', this.inputs)
      }
    }
  },
  mounted () {
    if (this.$attrs.value) {
      this.inputs = [...this.$attrs.value]
    }
  },
  name: 'InputGroup',
  props: ['type']
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
