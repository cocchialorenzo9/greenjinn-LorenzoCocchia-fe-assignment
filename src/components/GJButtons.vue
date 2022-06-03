<template>
  <div class="gj-buttons">
    <select v-model="firstTrade" @change="onChangeFirst">
      <option v-for="option in optionsFirst" :value="option" :key="option">
        {{ option }}
      </option>
    </select>
    /
    <select v-model="secondTrade" @change="onChangeSecond">
      <option v-for="option in optionsSecond" :value="option" :key="option">
        {{ option }}
      </option>
    </select>
  </div>
  <div class="gj-selected-trades">
    <GJNumbersView :title="'Choose a trade pair'"  :gjList="selectedTradeList" ></GJNumbersView>
  </div>
</template>

<script>
import axios from "axios";
import GJNumbersView from "@/components/GJNumbersView";

export default {
  name: "GJButtons",
  components: {GJNumbersView},

  data() {
    return {
      tradingPairs: null,
      firstTrade: null,
      secondTrade: null,
      selectedTradeList: null,
    };
  },
  computed: {
    optionsFirst() {
      return this.tradingPairs.map(pair => {
        if(pair.trading === "Enabled") {
          return pair.name.split("/")[0];
        }
      });
    },
    optionsSecond() {
      return this.tradingPairs
          .filter(pair => pair.trading === "Enabled" && pair.name.split("/")[0] === this.firstTrade)
          .map(pair => pair.name.split("/")[1]);
    },
  },
  beforeCreate() {
    axios.get("https://www.bitstamp.net/api/v2/trading-pairs-info/")
        .then(response => {
          this.tradingPairs = response.data;
        })
        .catch(error => {
          console.log(error);
        });
  },
  methods: {
    onChangeFirst(event) {
      console.log(event.target.value);
      this.secondTrade = null;
    },
    onChangeSecond(event) {
      console.log(event.target.value);
      if(!this.firstTrade || !this.secondTrade) return 0;
      let tradingPairEncoded = this.firstTrade.toLowerCase() + this.secondTrade.toLowerCase();
      axios.get("https://www.bitstamp.net/api/v2/ticker/" + tradingPairEncoded + "/")
          .then(response => {
            this.selectedTradeList = [];
            for(let i = 0; i < response.data.length; i++) {
              this.selectedTradeList.push(response.data[i].map(element => element.last));
            }
            this.selectedTradeList.map(element => {
              return {
                number: element,
                description: this.getDescription()
              };
            });
          })
          .catch(error => console.log(error));
    },
    getDescription(){
      if(this.firstTrade && this.secondTrade){
        return this.tradingPairs.clone().filter(pair => pair.name === this.firstTrade + "/" + this.secondTrade)
            .map(pair => pair.description);
      }
    }
  }
}
</script>

<style scoped>

.gj-buttons{
  flex: auto;
  flex-direction: row;
}

</style>