<template>
  <div>
    <h3>Add an Alert</h3><br>
    <form  class="form-group align-content-center" @submit.prevent="addAlert">
      <label for="">Time interval (In minutes)</label>
      <select class="form-control" v-model="time_interval">
        <option :value="time_interval" :key="time_interval.id" v-for="time_interval in time_intervals">{{time_interval}}</option>
      </select><br>
      <input class="form-control" type="text" v-model="user_name" name="title" placeholder="Name"><br>
      <input class="form-control" type="text" v-model="email" name="title" placeholder="Email"><br>
      <input class="form-control" type="text" v-model="search_string" name="title" placeholder="Enter search keywords"><br>
      
      <input type="submit" value="Add" class="btn">
    </form>
  </div>
</template>

<script>
export default {
  name: "AddAlert",
  data() {
    return {
        //id: ""
        user_name: '',
        email: '',
        time_interval: '',
        search_string: '',
        time_intervals: [2, 10, 30]
        } 
  },
  methods: {
    addAlert(e) {
      e.preventDefault();
      const newAlert = {
        //id: this.id,
        user_name: this.user_name,
        email: this.email,
        time_interval: this.time_interval,
        search_string: this.search_string
      }
      // Send up to parent
      this.$emit('add-alert', newAlert);

      this.time_rate = '',
      this.user_name = '',
      this.email = '',
      this.search_string = ''
    },
    },
  }
</script>
<style scoped>
  div {
    padding: 30px;
  }
</style>



