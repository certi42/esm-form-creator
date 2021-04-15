<template>
  <div class="schedule form">
    <label id="schedule_id">Schedule: <input type="text" placeholder="Schedule ID" v-model="data.schedule_id"></label>
    <label id="start_date">Start: <input type="date" placeholder="Start Date" v-model="data.start_date"></label>
    <label id="end_date">End: <input type="date" placeholder="End Date" v-model="data.end_date"></label>
    <label id="expiration">Expiration: <input type="number" placeholder="Expiration" v-model="data.expiration"></label>
    <div> Hours:
      <input-group type="number" v-model="data.hours"/>
    </div>
    <label id="interface">Interface: <input type="number" placeholder="Interface" v-model.number="data.interface"></label>
    <label id="notification_title">Notification Title: <input type="text" placeholder="Notification Title" v-model="data.notification_title"></label>
    <label id="notification_body">Notification Body: <input type="text" placeholder="Notification Body" v-model="data.notification_body"></label>
    <label id="randomize">Randomize: <input type="number" placeholder="Randomize" v-model.number="data.randomize"></label>
    <div> ESMs:
      <esm-group v-model="data.esms" :line="true"/>
    </div>
  </div>
</template>

<script>
import EsmGroup from './EsmGroup.vue'
import InputGroup from './InputGroup.vue'
export default {
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
      }
    }
  },
  watch: {
    data: {
      deep: true,
      handler () {
        this.$emit('input', this.data)
      }
    }
  },
  created () {
    this.$emit('input', this.data)
  },
  components: { EsmGroup, InputGroup }

}
</script>

<style scoped>
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
