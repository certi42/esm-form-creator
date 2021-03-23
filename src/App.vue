<template>
  <div id="app">
    <h1>ESM Generator</h1>
    <div class="panes">
      <div class="form">
        <label id="schedule_id">Schedule: <input type="text" placeholder="Schedule ID" v-model="data.schedule_id"></label>
        <label id="start_date">Start: <input type="date" placeholder="Start Date" v-model="data.start_date"></label>
        <label id="end_date">End: <input type="date" placeholder="End Date" v-model="data.end_date"></label>
        <label id="expiration">Expiration: <input type="number" placeholder="Expiration" v-model="data.expiration"></label>
        <div> Hours:
          <input-group type="number" v-model="data.hours"/>
        </div>
        <label id="interface">Interface: <input type="number" placeholder="Interface" v-model="data.interface"></label>
        <label id="notification_title">Notification Title: <input type="text" placeholder="Notification Title" v-model="data.notification_title"></label>
        <label id="notification_body">Notification Body: <input type="text" placeholder="Notification Body" v-model="data.notification_body"></label>
        <label id="randomize">Randomize: <input type="number" placeholder="Randomize" v-model="data.randomize"></label>
        <div> ESMs:
          <esm-group v-model="data.esms"/>
        </div>
      </div>
      <div class="json">
        <pre>{{ json }}</pre>
      </div>
    </div>
  </div>
</template>

<script>
import EsmGroup from './components/EsmGroup.vue'
import InputGroup from './components/InputGroup.vue'

export default {
  name: 'App',
  data () {
    return {
      data: {
        schedule_id: '',
        start_date: '',
        end_date: '',
        expiration: '',
        hours: [],
        interface: '',
        notification_title: 'EDIT HERE',
        notification_body: 'EDIT HERE',
        randomize: '',
        esms: []
      },
      json: ''
    }
  },
  methods: {
    renderJson () {
      // deep copy
      const clone = { ...this.data }
      const newEsms = []
      for (const esm of this.data.esms) {
        const newEsm = {}
        Object.entries(esm.data).forEach(([key, value]) => {
          newEsm['esm_' + key] = value
        })
        newEsms.push(newEsm)
      }

      clone.esms = newEsms
      this.json = JSON.stringify(clone, undefined, 2)
    }
  },
  created () {
    this.$watch('data', this.renderJson, { deep: true })
    this.renderJson()
  },
  components: {
    InputGroup,
    EsmGroup
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

.form {
  display: flex;
  flex-direction: column;
  width: max-content;
  flex-shrink: 1;
}

.form div {
  margin: 5px;
}

.form input {
  margin-left: 10px;
  flex-grow: 1;
}
.form label {
  display: flex;
  margin: 5px;
}

</style>
