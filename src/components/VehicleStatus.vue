<template>
   <div id="vehicle-status-table" class="app">
      <mdb-datatable
        :data="data"
        striped
        bordered
        arrows
        :display="3"
        reactive
        :time="7000"
        refresh
      />
  </div>
</template>

<script>
import { mdbDatatable, mdbContainer } from 'mdbvue';

let rows = [
              {
                name: 'Tiger Nixon',
                position: 'System Architect',
                office: 'Edinburgh',
                age: '61',
                date: '2011/04/25',
                salary: '$320'
              },
              {
                name: 'Garrett Winters',
                position: 'Accountant',
                office: 'Tokyo',
                age: '63',
                date: '2011/07/25',
                salary: '$170'
              }
            ];

let columns = [
              {
                label: 'Name',
                field: 'name',
                sort: 'asc'
              },
              {
                label: 'Position',
                field: 'position',
                sort: 'asc'
              },
              {
                label: 'Office',
                field: 'office',
                sort: 'asc'
              },
              {
                label: 'Age',
                field: 'age',
                sort: 'asc'
              },
              {
                label: 'Start date',
                field: 'date',
                sort: 'asc'
              },
              {
                label: 'Salary',
                field: 'salary',
                sort: 'asc'
              }
            ] 
let dataDinanmic
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
        columns: [],
        rows: []
      };
  },
  computed: {
      data() {
        return {
          columns: columns,
          rows: rows
        };
      },
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
