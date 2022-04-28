<template>
  <div>
    <input v-model="branch" type="number" placeholder="Branch No" />
    <input v-model="item_no" type="number" placeholder="Item No" />
    <input v-model="sales" type="number" placeholder="Sales" />
    <button @click="addData()">submit</button>
    <table>
      <thead>
        <tr>
          <td>Branch Number</td>
          <td>one</td>
          <td>two</td>
          <td>three</td>
          <td>four</td>
          <td>five</td>
          <td>six</td>
          <td>seven</td>
          <td>eight</td>
          <td>nine</td>
          <td>ten</td>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item, index) in store" :key="index">
          <td>{{ item.branch }}</td>
          <td v-for="(a, index) in item.sales" :key="index">{{ a }}</td>
          <!-- <td>
            {{ item.sales_figure.item_no == "1" ? item.sales_figure.sales : 0 }}
          </td>
          <td>
            {{ item.sales_figure.item_no == "2" ? item.sales_figure.sales : 0 }}
          </td>
          <td>
            {{ item.sales_figure.item_no == "3" ? item.sales_figure.sales : 0 }}
          </td>
          <td>
            {{ item.sales_figure.item_no == "4" ? item.sales_figure.sales : 0 }}
          </td>
          <td>
            {{ item.sales_figure.item_no == "5" ? item.sales_figure.sales : 0 }}
          </td>
          <td>
            {{ item.sales_figure.item_no == "6" ? item.sales_figure.sales : 0 }}
          </td>
          <td>
            {{ item.sales_figure.item_no == "7" ? item.sales_figure.sales : 0 }}
          </td>
          <td>
            {{ item.sales_figure.item_no == "8" ? item.sales_figure.sales : 0 }}
          </td>
          <td>
            {{ item.sales_figure.item_no == "9" ? item.sales_figure.sales : 0 }}
          </td>
          <td>
            {{
              item.sales_figure.item_no == "10" ? item.sales_figure.sales : 0
            }}
          </td> -->
        </tr>
      </tbody>
    </table>
  </div>
</template>
<script>
export default {
  /* eslint-disable */
  name: "App",
  data() {
    return {
      branch: "",
      item_no: null,
      sales: null,
      store: [],
    };
  },
  methods: {
    addData() {
      let data = {
        branch: this.branch,
        sales: [],
      };
      let item = this.store.find((item) => item.branch == this.branch);
      if (item) {
        item.sales[+this.item_no - 1] = this.sales;
      } else {
        data.sales.push(this.sales);
        this.store.push(data);
      }
    },
  },
};
</script>
<style>
input {
  margin-top: 1rem;
  display: block;
}
button {
  margin-top: 16px;
}
</style>
