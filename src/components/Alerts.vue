<template>
  <div>
    <div v-bind:key="alert.id" v-for="(alert, i) in alerts">
      <AlertItem v-bind:alert="alert" v-on:del-alert="$emit('del-alert', alert._id, i)" @alert="test"/>
    </div>
  </div>
</template>

<script>
import AlertItem from './AlertItem.vue';

export default {
  data() {
    return {
    }
  },
  name: "Alerts",
  components: {
    AlertItem
  },
  props: ["alerts"], 
  methods: {

  }
}
</script>

<style scoped>

</style>

