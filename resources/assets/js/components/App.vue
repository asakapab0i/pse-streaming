<template>
    <div>
        <app-nav></app-nav>
        <div class="container">
            <!-- <app-header></app-header> -->
            <!-- <div class="bs-docs-section clearfix"> -->
                <div class="page-header">
                    <div class="row">
                        <div class="col-lg-12">
                            <h1>Trending Stocks <img :src="require('../../img/svg/candle_sticks.svg')"/></h1>
                        </div>
                    </div>
                </div>
                <app-stocks></app-stocks>
            <!-- </div> -->
            <app-footer></app-footer>
        </div>
    </div>
</template>

<script>
window.Vue = require('vue');
Vue.component('app-nav', require('./Navigation.vue'))
Vue.component('app-header', require('./Header'))
Vue.component('app-footer', require('./Footer.vue'))
Vue.component('app-stocks', require('./Stocks/Index.vue'));

export default {
  mounted() {
    // console.log("Component mounted.");
  }
};
</script>
