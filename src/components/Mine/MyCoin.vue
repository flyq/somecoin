<template>
  <div>
    <img style="margin-left:30%;" alt="" width="40%" srcset="../../../static/pic/我的纪念币页面主图.png"/>
    <!-- <img style="margin-left:35%;" alt="" width="30%" srcset="../../../static/pic/我的纪念币页面按钮图.png"/> -->
    <div class="div1">
        <a @click="gotoExchangePage(type)">
          <span class="span1">{{$t('mine_exchange')}}</span>
          <img src="../../../static/pic/我的纪念币页面按钮图.png" class="img1" alt="" />
        </a>
      </div>
    <div v-for="(coin, index) in coins" :key="index">
      <br/>
      <div style="text-align: center;">{{coin.name}}</div>
      <img style="width: 80%;margin-left: 10%;" :src="coin.url" alt="" />
      <div style="text-align: center;">{{$t('mine_serial_number')}}{{coin.coinnumber}}</div>
      <div class="div2">
        <a @click="gotoSellPage(coin.coinnumber)">
          <span class="span1">{{$t('mine_sell')}}</span>
          <img src="../../../static/pic/我的纪念币页面按钮图.png" class="img1" alt="" />
        </a>
      </div>
    </div>
    <br/>
  </div>
</template>

<script>
import { mapActions, mapState } from 'vuex';

export default {
  name: 'mycoin',
  data () {
    return {
      coins: [],
      type: ""
    }
  },
  created: function () {
    const allcoins = this.existcoins;
    this.type = this.$route.params.cointype;
    for(const coinid in allcoins){
      const coin = allcoins[coinid];
      // console.log(this.$route.params.type + "," + coin.type + "," + this.$route.params.cointype + "," + coin.cointype + "," + this.$route.params.value + "," + coin.value);
      if(this.$route.params.type == coin.type &&
        this.$route.params.cointype == coin.cointype &&
        this.$route.params.value == coin.value &&
        this.scatterAccount.name == coin.owner){
          this.coins.push(coin);
        }
    }
  },
  methods:{
    gotoExchangePage(type){
      this.$router.push({ path: `/exchangecoin/${type}`});
    },
    gotoSellPage(coinnumber){
      this.$router.push({ path: `/sellcoin/${coinnumber}`});
    }
  },
  computed: {
    ...mapState(['existcoins','scatterAccount']),
  },
}
</script>

<style scoped>
/*div1下面 包含着1个图片和1段文字*/
  .div1{
      position: relative;/*相对定位*/
      width: 20%;
      /* height: 140px; */
      margin-left: 40%;
  }
  .div2{
      position: relative;/*相对定位*/
      width: 12%;
      /* height: 140px; */
      margin-left: 44%;
  }
  /*图片部分的设置*/
  .img1{
      /*position: static;默认定位,可以省略*/
      width: 100%;
      height: 40px;
  }
  /*文字的设置*/
  .span1{
      position: absolute;/*绝对定位*/
      width: 100%;
      bottom: 11px;/*离底下0像素*/
      left: 0px;/*离左边0像素*/
      text-align: center;
      font-size: 18px;
  }
</style>
