<template>
    <div ref="imageDom">
      <img id="profilePic" alt="Vue logo" src="./assets/profilePic.jpeg" />
      <HelloWorld msg="Hi dear" />

      <div id="crypto">
        <cryptoPrice v-bind:XTZ="XTZ" v-bind:ADA="ADA" />
      </div>
   
    <button id="button" @click="toImage">Download PDF</button>

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
import HelloWorld from "./components/HelloWorld.vue";
import qr from "./components/qr.vue";
import TwitterFeed from "./components/TwitterFeed.vue";
import cryptoPrice from "./components/cryptoPrice.vue";
import jsPDF from "jspdf";
import axios from "axios";
import html2canvas from "html2canvas";

export default {
  components: { HelloWorld, qr, cryptoPrice, TwitterFeed },
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
      this.BURST = apiCall.data.BURST.USD.toString();
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

  created() {
    // Stub
    this._getCryptoPrice();
    this.timer()
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 20px;
  /* background-color:black */
}
#profilePic {
  width: 200px;
  height: 200px;
  border-radius: 100px;
  border: 1px solid black;
}
#tweet {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  margin: auto;
  width: 500px;
  /* height: 300px; */
}
button{margin-top: 20px;}
a{margin:5px}
</style>
