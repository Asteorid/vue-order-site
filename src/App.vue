<template>
  <div id="app">
    <h1>Оформление заказа</h1>
    <ProductList @update-total="updateTotal" />
    <OrderForm :total="total" />
  </div>
</template>

<script>
import ProductList from './components/ProductList.vue';
import OrderForm from './components/OrderForm.vue';

export default {
  data() {
    return {
      total: 0
    };
  },
  methods: {
    updateTotal(newTotal) {
      this.total = newTotal;
    }
  },
  components: {
    ProductList,
    OrderForm
  }
};
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  text-align: center;
  margin-top: 40px;
}
</style>
