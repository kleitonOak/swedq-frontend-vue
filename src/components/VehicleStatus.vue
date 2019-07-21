<template>
   <div id="vehicle-status-table" class="app">
    <mdb-container>
      <mdb-datatable
        :data="data"
        striped
        bordered
        arrows
        :display="10"
        tfoot:false
        reactive
        :time="7000"
      />
    </mdb-container>
  </div>
</template>

<script>
import { mdbDatatable, mdbContainer } from 'mdbvue';
import axios from 'axios'

let customer_url = 'http://localhost:8082/api/v1/customer'
let vehicle_url = 'http://localhost:8081/api/v1/vehicle'

export default {
  name: 'VehicleStatus',
  props: {
    msg: String
  },
  components: {
      mdbDatatable,
      mdbContainer
  },
  data() {
      return {
        rows: [],
        columns: []
      };
  },
  computed: {
      data() {
        return {
          columns: this.columns,
          rows: this.rows
        };
      },
  },
  methods: {
    customerRequest() {
     return axios.get(customer_url)
    },
    vehicleRequest() {
      return axios.get(vehicle_url)
    },
    filterData(dataArr, keys) {
        let data = dataArr.map(entry => {
          let filteredEntry = {};
          keys.forEach(key => {
            if (key in entry) {
              filteredEntry[key] = entry[key];
            }
          });
          return filteredEntry;
        });
        return data;
    }
  },
  mounted(){
    axios.all([
        this.customerRequest(),
        this.vehicleRequest()
      ])
    .then(axios.spread((customer_response, vehicle_response) => {
          this.message = 'Request finished'
          let jsonMerged = mergeJsonData(customer_response.data, vehicle_response.data);
          let keys = ["name", "idVehicle", "status"];
          let entries = this.filterData(jsonMerged, keys);
          //columns
          this.columns = keys.map(key => {
            return {
              label: key.toUpperCase(),
              field: key,
              sort: 'asc'
            };
          });
          //rows
          entries.map(entry => this.rows.push(entry));
     })).catch(err => console.log(err));
  }
}

function mergeJsonData(customers, vehicles){
  let dataMerge = []
  for(const vehicle of vehicles) {
    for(const customer of customers){
       if(customer.id === vehicle.idCustomer){
        const mergedTarget = Object.assign({},vehicle, customer);
        dataMerge.push(mergedTarget)
       }
    }
  }
  return dataMerge
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
