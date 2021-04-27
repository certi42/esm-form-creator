<template>
  <div id="app">
    <h1 class="title">ESM Generator</h1>
    <h3 class="subtitle">Click '+' to add a schedule</h3>
    <div class="panes">
      <schedule-group v-model="schedules"/>
      <div class="json">
        <pre>{{ json }}</pre>
      </div>
    </div>
  </div>
</template>

<script>
import ScheduleGroup from './components/ScheduleGroup.vue'

export default {
  name: 'App',
  data () {
    return {
      schedules: [],
      json: ''
    }
  },
  methods: {
    renderJson () {
      this.json = JSON.stringify(this.schedules, undefined, 2)
    }
  },
  created () {
    this.$watch('schedules', this.renderJson, { deep: true })
    this.renderJson()
  },
  components: {
    ScheduleGroup
  }
}
</script>

<style scoped>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

.panes {
  display: flex;
  justify-content: space-between;
}

.json {
  width: 50%;
  border: 1px solid #5553;
  border-radius: 15px;
  padding: 10px;
  background: #5551;
}

.title {
  margin-bottom: 0;
}
.subtitle {
  margin-top: 0;
  color: #627385;
  font-weight: normal;
}
</style>
