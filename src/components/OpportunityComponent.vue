<template>
  <div class="container-fluid">
    <div class="p-3">
      <h1>{{ title }}</h1>
    </div>

    <div class="container pt-2 pb-2">
      <div class="dropdown">
        <button
          class="btn btn-secondary dropdown-toggle"
          type="button"
          data-toggle="dropdown"
        >
          VIEW <span class="caret"></span>
        </button>
        <div class="dropdown-menu dropdown-menu-right">
          <a class="dropdown-item" href="javascript:void(0)"
            >Show full attributes</a
          >
          <a
            class="dropdown-item"
            href="javascript:void(0)"
            @click="changeList()"
            >Show monthly summary</a
          >
        </div>
      </div>
    </div>

    <div class="scrollable-table">
      <table class="table borderless text-nowrap" cellspacing="0">
        <thead>
          <tr>
            <th>Product</th>
            <th>Option</th>
            <th>Attribute</th>
            <th>Revenue Type</th>
            <th>QTY</th>
            <th>Unit Price</th>
            <th>Start Month</th>
            <th>Months</th>
            <th>Revenue Recognition</th>
            <th>Commited</th>
            <th
              v-show="check"
              v-for="(item, index) in yearSummary"
              :key="index"
            >
              {{ item.year }}
            </th>
            <th
              v-show="!check"
              v-for="(item, index) in yearSummary"
              :key="index"
            ></th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(item, index) in yearList" :key="index">
            <td>
              {{ item.productItemName ? item.productItemName : "-" }}
            </td>
            <td>{{ item.optionItemName ? item.optionItemName : "-" }}</td>
            <td>{{ item.attributes ? item.attributes : "-" }}</td>
            <td>{{ item.revenueType ? item.revenueType : "-" }}</td>
            <td>{{ item.qty ? item.qty : "-" }}</td>
            <td>{{ item.unitPrice ? item.unitPrice : "-" }}</td>
            <td>{{ item.startMonth ? item.startMonth : "-" }}</td>
            <td>{{ item.months ? item.months : "-" }}</td>
            <td>
              {{
                item.revenueRecognitionName ? item.revenueRecognitionName : "-"
              }}
            </td>
            <td>{{ item.committed ? item.committed : "-" }}</td>
            <td v-show="check">{{ item[2019] }}</td>
            <td v-show="check">{{ item[2020] }}</td>
            <td v-show="check">{{ item[2021] }}</td>
          </tr>
          <tr v-if="check">
            <td v-for="index in 10" :key="index"></td>
            <td v-for="(qwe, serial1) in yearSummary" :key="serial1">
              {{ qwe.summaryAmount }}
            </td>
          </tr>
          <tr v-if="!check">
            <td v-for="index in 10" :key="index"></td>
            <td
              v-for="(qwe, serial1) in monthSummary.summaryAmount"
              :key="serial1"
            >
              {{ qwe }}
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
import {
  lineItemData,
  summaryMonths,
  summaryYears,
} from "../assets/staticData/StaticData";
export default {
  name: "OpprtunityComponent",
  props: {
    title: String,
  },
  data() {
    return {
      lineItem: lineItemData,
      yearSummary: summaryYears.responseData.yearsData,
      monthSummary: summaryMonths.responseData,
      check: true,
    };
  },
  computed: {
    yearList() {
      let result = [];
      lineItemData.forEach((element) => {
        let d = element;
        summaryYears.responseData.yearsData.forEach((x) => {
          x.lineData.forEach((item) => {
            if (item.recordId === element.productFLIId) {
              d[x.year] = item.amount;
            }
          });
        });
        result.push(d);
      });
      return result;
    },
  },
  methods: {
    changeList: function () {
      this.check = !this.check;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

.container-fluid {
  padding: 0px !important;
}

.scrollable-table {
  overflow-x: auto;
}

/* see: https://stackoverflow.com/a/26983473 */
table {
  /* override Bootstrap's width */
  width: inherit !important;
  border-collapse: collapse;
}
tr {
  border-top: 2px solid #f2f2f2;
}
td,
th {
  padding: 1.5em;
  width: auto;
}
td.min,
th.min {
  width: 1% !important;
  white-space: nowrap !important;
}

thead {
  border-bottom: 3px solid #c3eb5b;
}

.dropdown {
  text-align: end;
}

.dropdown:hover > .dropdown-menu {
  display: block;
  float: right;
  right: 0;
  margin: 0px;
}

.dropdown > .dropdown-toggle:active {
  /*Without this, clicking will make it sticky*/
  pointer-events: none;
}

table tbody > tr:last-child {
  background: #f2f2f2;
}

.container {
  background: #f2f2f2;
  width: 100% !important;
}

@media (min-width: 576px) {
  .container {
    margin: 0px !important;
    max-width: 100%;
  }
}

@media (max-width: 330px) {
  .container-fluid {
    margin-top: 150px;
  }
}
</style>
