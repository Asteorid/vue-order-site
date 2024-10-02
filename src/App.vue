<template>
  <div id="app">
    <div class="container">
      <!-- Фильтры -->
      <div class="filters">
        <h3>Фильтры</h3>
        <div class="filter-item">
          <h4>Категории</h4>
          <label v-for="category in categories" :key="category">
            <input type="checkbox" :value="category" v-model="selectedCategories" />
            {{ category }}
          </label>
        </div>

        <div class="filter-item">
          <h4>Поиск по названию</h4>
          <input v-model="searchQuery" placeholder="Введите название" class="search-box" />
        </div>

        <div class="filter-item">
          <h4>Сортировка</h4>
          <label for="sort">Сортировать по:</label>
          <select v-model="sortBy" id="sort" class="dropdown">
            <option value="price">Цене</option>
            <option value="name">Названию</option>
          </select>
        </div>
      </div>

      <!-- Список товаров -->
      <div class="product-list">
        <h3>Товары</h3>
        <div v-for="product in filteredAndSortedProducts" :key="product.id" class="product-item">
          <p>{{ product.name }} - {{ product.price }}$</p>
          <button @click="addToCart(product)" class="btn">Добавить в корзину</button>
        </div>
      </div>

      <!-- Корзина -->
      <div class="cart">
        <h3>Корзина</h3>
        <p>Сумма заказа: {{ totalAmount }}$</p>
        <ul>
          <li v-for="product in cart" :key="product.id" class="cart-item">
            {{ product.name }} - {{ product.price }}$
            <button @click="removeFromCart(product.id)" class="btn-remove">Удалить</button>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      products: [
        { id: 1, name: 'Кроссовки A', category: 'Обувь', price: 100 },
        { id: 2, name: 'Кроссовки B', category: 'Обувь', price: 200 },
        { id: 3, name: 'Футболка A', category: 'Одежда', price: 50 },
        { id: 4, name: 'Футболка B', category: 'Одежда', price: 60 },
      ],
      categories: ['Обувь', 'Одежда'],
      selectedCategories: [],
      searchQuery: '',
      sortBy: 'price',
      cart: [],
    };
  },
  computed: {
    filteredAndSortedProducts() {
      let filtered = this.products.filter((product) => {
        return (
          this.selectedCategories.length === 0 ||
          this.selectedCategories.includes(product.category)
        );
      });

      filtered = filtered.filter((product) => {
        return product.name.toLowerCase().includes(this.searchQuery.toLowerCase());
      });

      if (this.sortBy === 'price') {
        return filtered.sort((a, b) => a.price - b.price);
      } else if (this.sortBy === 'name') {
        return filtered.sort((a, b) => a.name.localeCompare(b.name));
      }
      return filtered;
    },
    totalAmount() {
      return this.cart.reduce((sum, product) => sum + product.price, 0);
    },
  },
  methods: {
    addToCart(product) {
      this.cart.push(product);
    },
    removeFromCart(productId) {
      this.cart = this.cart.filter((product) => product.id !== productId);
    },
  },
};
</script>

<style scoped>
/* Общий контейнер */
.container {
  display: flex;
  justify-content: space-between;
  padding: 20px;
}

/* Секция фильтров */
.filters {
  width: 30%;
  padding: 10px;
  background-color: #f9f9f9;
  border: 1px solid #ccc;
  border-radius: 8px;
}

/* Фильтры: стили для элементов */
.filter-item {
  margin-bottom: 20px;
}

.search-box {
  width: 100%;
  padding: 8px;
  margin-top: 8px;
  border-radius: 4px;
  border: 1px solid #ccc;
}

.dropdown {
  width: 100%;
  padding: 8px;
  margin-top: 8px;
  border-radius: 4px;
  border: 1px solid #ccc;
}

/* Список товаров */
.product-list {
  width: 35%;
}

.product-item {
  padding: 10px;
  margin-bottom: 15px;
  border: 1px solid #eee;
  border-radius: 8px;
  background-color: #fff;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.btn {
  padding: 8px 12px;
  background-color: #4caf50;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.btn:hover {
  background-color: #45a049;
}

/* Корзина */
.cart {
  width: 30%;
  background-color: #fafafa;
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 8px;
}

.cart-item {
  margin-bottom: 10px;
  display: flex;
  justify-content: space-between;
}

.btn-remove {
  padding: 5px 10px;
  background-color: #f44336;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.btn-remove:hover {
  background-color: #e53935;
}
</style>
