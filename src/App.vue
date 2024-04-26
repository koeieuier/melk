<script setup>
import {reactive, ref} from 'vue'

const msg = ref('poing')
const product_list = ref([])
var product = ref([])
const total_price=ref(0)

function bounce() {
  msg.value = msg.value.concat(' poing')
  console.log(msg)
}

function add_product() {
  product = {
    name:document.getElementById("produkt").value,
    amount:document.getElementById("aantal").value,
    price:document.getElementById("prijs").value
  }
  product_list.value.push(product)
  calculate_total()
}

function calculate_total() {
  total = 0;
  product_list.value.forEach((product) => total += product.amount * product.price)
  total_price.value=total
}
</script>

<template>
  <h1>{{ msg }}</h1><br />
  <button @click="bounce()">bounce!</button>
  <br />
  <table>
    <tr>
      <th>Boodschappen</th>
    </tr>
    <tr>
      <td>produkt</td>
      <td>aantal</td>
      <td>prijs</td>
      <td>subtotaal</td>
    </tr>
    <tr>
      <td><input type="text" name="produkt" id="produkt"/></td>
      <td><input type="number" name="aantal" id="aantal"/></td>
      <td><input type="text" name="prijs" id="prijs"/></td>
      <td></td>
      <td><button @click="add_product">Toevoegen</button></td>
    </tr>
    <tr v-for="row in product_list" >
      <td>{{row.name}}</td>
      <td><input type="number" v-model="row.amount" v-on:change="calculate_total"/></td>
      <td class="price">&euro;{{ parseFloat(row.price).toFixed(2) }}</td>
      <td class="price">&euro;{{ parseFloat(row.price * row.amount).toFixed(2) }}</td>
    </tr>
    <tr>
      <td colspan="3">Totaal</td>
      <td id="total" class="price">&euro;{{ total_price.toFixed(2) }}</td>
    </tr>
    
  </table>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
