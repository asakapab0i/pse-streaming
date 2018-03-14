<template>
                  <div class="row">
                      <div v-for="(stock, index) in sortedArray" v-bind:key="index" class="col-lg-3">
                        <transition name="fade">
                          <div v-bind:class="{'' : stock.percent_change === 0, 'border-danger text-danger': stock.percent_change < 0,  'border-success text-success': stock.percent_change > 0}" class="card mb-3">
                              <div class="card-header font-weight-bold">{{stock.symbol}} <span> <i v-if="stock.percent_change < 0" class="fa fa-arrow-down" aria-hidden="true"></i>
                                      <i v-if="stock.percent_change > 0" class="fa fa-arrow-up" aria-hidden="true"></i> </span></div>
                              <div class="card-body">
                              <h4 class="card-title">{{stock.name}}</h4>
                              <p class="card-text">{{stock.price.currency}} {{stock.price.amount}}&nbsp; 
                                  <span><i class="fa fa-database" aria-hidden="true"></i>&nbsp;{{stock.volume}}</span>
                                  <span v-if="stock.percent_change !== 0" class="float-right">
                                      {{stock.percent_change}}&percnt;
                                  </span>
                              </p>
                              </div>
                          </div>
                          </transition>
                      </div>
                </div>
</template>
<style>
@-webkit-keyframes fade-enter-active {
0% { opacity: 1.0; }
50% { opacity: 0.0; }
100% { opacity: 1.0; }
}
@-moz-keyframes fade-enter-active {
0% { opacity: 1.0; }
50% { opacity: 0.0; }
100% { opacity: 1.0; }
}
.fade-enter-active,
.fade-leave-active {
  -webkit-animation: fade-enter-active 1s 2;
  -moz-animation: fade-enter-active 1s 2;
  animation: fade-enter-active 1s 2;
}

</style>

<script>
let _ = require("lodash");
export default {
  data: function() {
    return {
      stocks: {}
    };
  },
  computed: {
    sortedArray: function() {
      this.stocks = _.orderBy(this.stocks, ["volume", "percent_change"], ["desc", "asc"]);
      return this.stocks;
    }
  },
  mounted() {
    setInterval(
      () =>
        axios
          .get("/api/Stocks/")
          .then(response => (this.stocks = response.data.stock)),
      5000
    );
  }
};
</script>

