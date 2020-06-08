<template>
  <div id="app">
    <!-- <InventoryListing title="คลังสินค้า"/> -->
    <InventoryListingFetch title="คลังสินค้า"/>
  </div>
</template>

<script>
// import InventoryListing from "./components/InventoryListing";
import InventoryListingFetch from "./components/InventoryListingFetch";


export default {
  name: 'App',
  components: {
    // InventoryListing,
    InventoryListingFetch
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
