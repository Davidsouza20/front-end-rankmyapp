<template>
  <div id="app">
    <AddAlert v-if="!isEdit" v-on:add-alert="addAlert"/>
    <Alerts v-bind:alerts="alerts" v-on:del-alert="deleteAlert" />
  </div>
</template>


<script>
import Alerts from "../components/Alerts";
import AddAlert from "../components/AddAlert";
import axios from "axios";

export default {
  name: "Home",
  components: {
    Alerts,
    AddAlert
  },
  data() {
    return {
      alerts: [],
      isEdit: false
      
    };
  },
  
  //Ajax calls to the API
  methods: {
    deleteAlert(_id, i) {
      axios.delete(`http://localhost:5001/api/alert/${_id}`)
        .then(res => {this.alerts.splice(i, 1);})
        .catch(err => console.log(err));
    },
 
    addAlert(newAlert) {
      const data = Object.entries(newAlert)
        .map(([key, val]) => `${key}=${encodeURIComponent(val)}`)
        .join("&");
      const options = {
          headers: { "content-type": "application/x-www-form-urlencoded" },};
      axios.post("http://localhost:5001/api/alert", data, options)
          .then(res =>  this.alerts.unshift(res.data))  
          .catch(err => console.log(err));  
    },
  },

  //Display the list of Cars
  created() {
    axios
      .get("http://localhost:5001/api/alert")
      .then(res => (this.alerts = res.data))
      .catch(err => console.log(err));  
     
   
  },
};
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: Arial, Helvetica, sans-serif;
  line-height: 1.4;
}

.btn {
  display: inline-block;
  border: none;
  background: #555;
  color: #fff;
  padding: 7px 20px;
  cursor: pointer;
}

.btn:hover {
  background: #666;
}
</style>
