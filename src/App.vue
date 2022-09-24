<template>
  <div class="container">
    <div class="row">

<h1 class="text-center">Kev crypto </h1>


  <table class="table table-success table-striped">
    <thead>
      <tr>
        <th v-for="title in titles" :key="title">
          {{title}}
        </th>
        



      </tr>
    </thead>
    <tbody>
      <tr v-for="(coin, index) in coins" :key="coin.id">
        <td class="text-muted">
        {{index+1}}
      </td>
      <td>
        <img :src="coin.image" style="width:2rem" class="me-2">
        <span>
        {{
        coin.name
      }}
        </span>
<span class="ms-2 text-uppercase text-muted">
{{
  coin.symbol
}}
</span>
      </td>
      <td>
        {{coin.current_price}}
      </td>
      <td>
        {{coin.price_change_percentage_24h}}%
      </td>
      <td>
        $ s{{coin.total_volume}}
      </td>
      </tr>
    </tbody>

  </table>

    </div>
  </div>
</template>

<script>


export default {
  name: 'App',
  data(){
  return{
      coins:[],
      titles: [
        "#",
        "Coins",
        "Price",
        "Price Charge",
        "24h volume",

      ],
      textSearch:"",
    };

  },
    async mounted(){
      const res = await fetch('https://api.coingecko.com/api/v3/coins/markets?vs_currency=usd&order=market_cap_desc&per_page=100&page=1&sparkline=false')
        const data = await res.json()
      console.log(data)
      this.coins=data;
   },

metodos:{

//Analizar el bug del buscador no esta 
// funcionando...
   searchCoin(){
    this.coins=this.coins.filter((coin) => 
    coin.name.toLowerCase().includes(this.textSearch.toLowerCase())||
    coin.symbol.toLowerCase().includes(this.textSearch.toLowerCase())
    );
   },
   },
};
</script>

<style>

</style>
