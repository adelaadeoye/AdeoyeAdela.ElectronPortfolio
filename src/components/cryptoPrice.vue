<template>
  <div>
    <h2>Current prices of coins</h2>

    <div id="crypto">
      <div>
        <h4>TEZOS</h4>
        <p>${{ XTZ }}</p>
        <vue-qrcode :value="'The price of TEZOS is $'+XTZ" scale="2" />
      </div>
      <div>
        <h4>BURST</h4>
        <p>${{ BURST }}</p>
        <vue-qrcode :value="'The price of BURST is $' + BURST" scale="2" />
      </div>
      <div>
        <h4>CARDANO</h4>
        <p>${{ ADA }}</p>
        <vue-qrcode :value="'The price of ADA is $' + ADA" scale="2"/>

      </div>
    </div>
  </div>
</template>

<script>
import VueQrcode from "vue-qrcode";

export default {
  name: "app",
  props: {
    XTZ: { type: String },
    ADA: { type: String },
    BURST: { type: String },
  },
  data() {
    return {};
  },
  components: {
    VueQrcode,
  },
};
</script>
<style scoped>
.currency {
  border: 1px solid #f5ce00;
  border-radius: 15px;
  padding: 2em 0em;
  display: inline-block;
  width: 30%;
}
div p {
  font-size: 2rem;
}
h2 {
  font-size: 1.5em;
}
#crypto {
  display: flex;
  flex-direction: row;
  justify-content: space-around;
  margin: auto;
  width: 400px;
}
</style>
