<template>
  <div class="stock">
    <div class="stock-item" v-for="value in stock" :key="value.stock">
      <div class="stock-item__info">
        <div class="stock-item__cover">
          <img :src="value[0].image" :alt="value[0].companyName">
        </div>
        <h3 class="stock-item__title">
          {{ value[0].companyName }}
          <span>{{ value[0].symbol }}</span>
        </h3>
      </div>
      <span class="stock-item__price">{{ value[0].price }} $</span>
    </div>
  </div>

  <h3>Get info</h3>

  <select v-model="selected">
    <option value="" disabled>Select company</option>
    <option v-for="value in stock" :key="value[0].stock" :value="value[0].description">{{ value[0].companyName }}</option>
  </select>

  <div class="info">
    {{ selected }}
  </div>
</template>

<script>
  import axios from 'axios'

  export default {
    name: 'Stocks',
    data() {
      return {
        stock: [],
        errors: [],
        selected: ''
      }
    },
    created() {
      const tickers = [
        'AAPL',
        'WISH',
        'SPCE',
        'CLNE',
        'CLOV',
        'PLTR'
      ];

      tickers.forEach(ticker => {
        axios.get(`https://financialmodelingprep.com/api/v3/profile/${ticker}?apikey=2c27319e1f56b1407987218b594f7b24`)
        .then(response => {
          this.stock.push(response.data)
        })
        .catch(e => {
          this.errors.push(e)
        })
      });
    }
  }
</script>
