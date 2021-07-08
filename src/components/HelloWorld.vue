<template>
  <div ref="imageDom">
    <img id="profilePic" alt="My profile pic" src="../assets/profilePic.jpeg" />

    <h1>{{ msg }}</h1>

    <h2>My Name is Adela Adeoye</h2>
    <vue-qrcode value="Adela Adeoye" scale="2" />

    <p class="">
      Are you into Crypto 🤑 I have got the latest price for you 😉
    </p>
    <div id="crypto">
      <cryptoPrice v-bind:XTZ="XTZ" v-bind:ADA="ADA" />
    </div>
    <button id="button" @click="toImage">Download page As png</button>

    <div id="tweet">
      <TwitterFeed
        src="https://twitter.com/BBCAfrica?ref_src=twsrc%5Etfw"
      ></TwitterFeed>
      <TwitterFeed
        src="https://twitter.com/ethereum?ref_src=twsrc%5Etfw"
      ></TwitterFeed>
    </div>
    <a href="https://github.com/adelaadeoye" target="blank">Github</a>
      <a href="https://www.linkedin.com/in/adeoyeadela/" target="blank">linkedin</a>
      <a href="mailto:adeoye.adela@gmail.com">email</a>
      <a href="https://drive.google.com/file/d/1AVRk37NOH5KCTfqbgi0QIZFPRiNykNBS/view?usp=sharing" target="blank">Resume</a>
   
  </div>
</template>
<script>
import VueQrcode from "vue-qrcode";
import cryptoPrice from "./cryptoPrice.vue";
import TwitterFeed from "./TwitterFeed.vue";
import html2canvas from "html2canvas";
import jsPDF from "jspdf";
import axios from "axios";
export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },
  data() {
    return {
      XTZ: "",
      BURST: "",
      ADA: "",
    };
  },
  methods: {
    async _getCryptoPrice() {
      let apiCall = await axios.get(
        "https://min-api.cryptocompare.com/data/pricemulti?fsyms=XTZ,BURST,ADA&tsyms=USD"
      );

      this.XTZ = apiCall.data.XTZ.USD.toString();
      this.ADA = apiCall.data.ADA.USD.toString();
      this.BURST = apiCall.data.BURST.USD.toString()?apiCall.data.BURST.USD.toString():"NA";
    },
    timer() {
      setInterval(() => {
        this._getCryptoPrice();
      }, 5000);
    },

    toImage() {
      html2canvas(this.$refs.imageDom, {
        backgroundColor: "#ffffff",
      }).then((canvas) => {
        var imgData = canvas.toDataURL("image/jpeg");
        this.fileDownload(imgData);
      });
    },
    fileDownload(downloadUrl) {
      let aLink = document.createElement("a");
      aLink.style.display = "none";
      aLink.href = downloadUrl;
      aLink.download = "File.png";
      document.body.appendChild(aLink);
      aLink.click();
      document.body.removeChild(aLink);
    },
  },
  components: {
    VueQrcode,
    cryptoPrice,
    TwitterFeed,
  },
  created() {
    // Stub
    this._getCryptoPrice();
    this.timer();
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
#tweet {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  margin: auto;
  width: 500px;
  /* height: 300px; */
}
button {
  margin-top: 20px;
}
a {
  margin: 5px;
}
</style>
