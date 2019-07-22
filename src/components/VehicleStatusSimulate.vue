<template>
   <div id="vehicle-status-simulate-table" class="app">
     <p>
       
          1) Click on Simulate Button to Random 3 Online Vehicles
          <br>
          2) Change to Vehicle Status Tab to see the result
          <br>
          3) Click on Refresh button
     </p>
    <button @click="randomVehicleStatus()" title="Simulate Random Online Vehicles!" type="button" class="btn btn-primary">Simulate</button> 
  </div>
</template>

<script>
import axios from 'axios'
let vehicle_status_url = 'http://localhost:8083/api/v1/vehicle/status/'
let vehicle_url = 'http://localhost:8081/api/v1/vehicle'
export default {
  name: 'VehicleStatusSimulate',
  props: {
  },
  components: {
  },
  data() {
      return {
      };
  },
  computed: {
  },
  methods: {
    randomVehicleStatus() {
        axios.get(vehicle_url).then(function(response){
          let data = response.data;
          if (data && data.length) { 
           let randomPosition = [];
            randomPosition.push(Math.floor(Math.random() * data.length));
            randomPosition.push(Math.floor(Math.random() * data.length));
            randomPosition.push(Math.floor(Math.random() * data.length));
            randomPosition.forEach(position => {
                  axios.post(vehicle_status_url+data[position].idVehicle) 
            });
          }
        });  
    }
  }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.list-group-item {
    display: list-item;
}
</style>