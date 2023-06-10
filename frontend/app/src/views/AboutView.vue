<template>
  <div>
  <h1>今日のあなたの運勢は．．．</h1>
  <p>’{{ message }}’です！</p>
  <h2>今日のラッキーアイテムはこちら！</h2>
  <div>
    <div v-if="product">
      <h2>{{ product.itemName }}</h2>
      <img :src="product.mediumImageUrls[0]" :alt="product.itemName" />
      <p>{{ product.itemPrice }}円</p>
      <a :href="product.itemUrl" target="_blank">商品ページを見る</a>
    </div>
    <div v-else>
      <p>商品を取得しています...</p>
    </div>
  </div>
</div>

</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      product: null
    };
  },

  computed: {
    message() {
      
      const RN = Number(this.$route.params.seed)
      
      if (RN % 7 === 0) {
        return '大吉'
      } else if(RN % 7 === 1) {
        return '中吉'
      } else if(RN % 7 === 2) {
        return '小吉'
      } else if(RN % 7 === 3){
        return '凶'
      } else if(RN % 7 === 4){
        return '大凶'
      } else {
        return 'かなりヤバい'
      }
    }
  },

  async created() {
  try {
    const apiKey = YOUR_API_KEY;
    const genreId = 567679; // RakutenのジャンルID
    const response = await axios.get(`https://app.rakuten.co.jp/services/api/IchibaItem/Search/20170706?format=json&applicationId=${apiKey}&genreId=${genreId}`);
    const products = response.data.Items;
    
    if (products && products.length > 0) {
      const randomIndex = Math.floor(Math.random() * products.length);
      this.product = products[randomIndex];
    } else {
      console.error('No products found.');
    }
  } catch (error) {
    console.error(error);
  }
}

}
</script>
<style>
.pane{
  background-size: cover;
  background-color: #ffffff00;
}
</style>