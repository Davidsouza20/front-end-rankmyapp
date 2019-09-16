<template>
  <div class="todo-item">
    <p><strong>Name:</strong> {{ alert.user_name }} <br> 
      <strong>Email:</strong> {{ alert.email }} <br> 
      <strong>Time Interval:</strong> {{ alert.time_interval}} Minutes <br>
      <strong>Search Keywords:</strong> {{ alert.search_string }}
      <button @click="$emit('del-alert', alert._id)" class="btn btn-danger btn-sm pull-right margin red">x</button>
      </p>  
      <span v-if="show">
      <EditAlert @edited-alert="updateAlert" />
      </span>
  </div>
</template>
                               
<script>
export default {
  data: function() {
    return {
      show: false,
        alerts: []
    }
  },  
  components: {
  },
  name: "AlertItem",
  props: ["alert"],

  methods: {
    updateAlert(newAlert) {
      console.log(newAlert);
      const _id =  this.alert._id;
      this.$emit('alert', newAlert, _id);
      this.show = false;
    },
    isActive() {
      this.show = !this.show
    }
      
  }
}
</script>

<style scoped>
  .todo-item {
    background: #f4f4f4;
    margin: 10px;
    padding: 10px;
    border-bottom: 1px #ccc dotted;
  }

  .is-complete {
    text-decoration: line-through;
  }

  .margin {
    margin: 0 5px;
  }

  .yellow {
    background-color: yellow;
    color:#000;
  }

  .red {
    background-color: red;
  }
</style>

