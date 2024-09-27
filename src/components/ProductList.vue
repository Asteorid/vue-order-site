<template>
  <div>
    <h2>Список товаров</h2>
    <ul>
      <li v-for="(product, index) in products" :key="index">
        {{ product.name }} - {{ product.price }}$
        <button @click="addToCart(index)">Добавить</button>
        <button @click="removeFromCart(index)" :disabled="product.quantity === 0">Удалить</button>
        Количество в корзине: {{ product.quantity }}
      </li>
    </ul>
    <p>Общая сумма: {{ total }}$</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      products: [
        { name: 'Картошка', price: 100, quantity: 0 },
        { name: 'Помидор', price: 200, quantity: 0 },
        { name: 'Лук', price: 300, quantity: 0 }
      ],
      total: 0
    };
  },
  methods: {
    addToCart(index) {
      this.products[index].quantity++;
      this.calculateTotal();
    },
    removeFromCart(index) {
      if (this.products[index].quantity > 0) {
        this.products[index].quantity--;
        this.calculateTotal();
      }
    },
    calculateTotal() {
      this.total = this.products.reduce((acc, product) => acc + (product.price * product.quantity), 0);
      this.$emit('update-total', this.total);
    }
  }
};
</script>

<style>
ul {
  list-style-type: none;
  padding: 0;
}

button {
  margin-left: 10px;
}
</style>
