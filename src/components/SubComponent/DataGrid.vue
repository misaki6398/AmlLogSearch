<template>
<div>
  <table class="table-body table-color">
    <thead>
      <tr class="table-tr">
        <th v-for="column in columns"
          @click="sortBy(column)"
          :class="{ active: sortKey == column }"
          class="table-th">
          {{ column | capitalize }}
          <span class="arrow" :class="sortOrders[column] > 0 ? 'asc' : 'dsc'">
          </span>
        </th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="(entry,index) in filteredData" class="table-tr">
        <td v-for="column in columns" :key="column" class="table-td">
          <!-- {{entry[index][column]}}           -->
          {{entry[column]}} 
        </td>
      </tr>
    </tbody>
  </table>
</div>
   
</template>

<script>
  export default {
    props: {
        data: Array,
        columns: Array,
        filterKey: String
      },
      data: function () {
        var sortOrders = {}
        this.columns.forEach(function (key) {
          sortOrders[key] = 1
        })
        return {
          sortKey: '',
          sortOrders: sortOrders
        }
      },
      computed: {
        filteredData: function () {
          var sortKey = this.sortKey
          var filterKey = this.filterKey && this.filterKey.toLowerCase()
          var order = this.sortOrders[sortKey] || 1
          var data = this.data
          if (filterKey) {
            data = data.filter(function (row) {
              return Object.keys(row).some(function (key) {
                return String(row[key]).toLowerCase().indexOf(filterKey) > -1
              })
            })
          }
          if (sortKey) {
            data = data.slice().sort(function (a, b) {
              a = a[sortKey]
              b = b[sortKey]
              return (a === b ? 0 : a > b ? 1 : -1) * order
            })
          }
          return data
        }
      },
      filters: {
        capitalize: function (str) {
          return str.charAt(0).toUpperCase() + str.slice(1)
        }
      },
      methods: {
        sortBy: function (key) {
          this.sortKey = key
          this.sortOrders[key] = this.sortOrders[key] * -1
        }
      }
  } 
</script>

<style>
.table-body {
  font-family: Helvetica Neue, Arial, sans-serif;
  font-size: 14px;
  color: #444;
}

.table-color {
  border: 2px solid #128bca;
  border-radius: 3px;
  background-color: #fff;
}

.table-th {
  background-color: #428bca;
  color: rgba(255,255,255,0.66);
  cursor: pointer;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.table-td {
  background-color: #f9f9f9;
}

.table-th, .table-td {
  min-width: 100%;
  max-width: 100%;
  padding: 10px 20px;
}

.table-th, .table-tr {
  min-width: 100%;
  max-width: 100%;
}

.table-th.active {
  color: #fff;
}

.table-th.active .arrow {
  opacity: 1;
}

.arrow {
  display: inline-block;
  vertical-align: middle;
  width: 0;
  height: 0;
  margin-left: 5px;
  opacity: 0.66;
}

.arrow.asc {
  border-left: 4px solid transparent;
  border-right: 4px solid transparent;
  border-bottom: 4px solid #fff;
}

.arrow.dsc {
  border-left: 4px solid transparent;
  border-right: 4px solid transparent;
  border-top: 4px solid #fff;
}

</style>
