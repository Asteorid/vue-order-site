<template>
    <div>
      <h2>Заполните форму заказа</h2>
      <form @submit.prevent="submitOrder">
        <div>
          <label for="name">Имя:</label>
          <input type="text" v-model="name" required />
        </div>
        <div>
          <label for="email">Email:</label>
          <input type="email" v-model="email" required />
        </div>
        <div>
          <label for="address">Адрес:</label>
          <input type="text" v-model="address" required />
        </div>
        <div>
          <p>Сумма заказа: {{ total }}$</p>
        </div>
        <button type="submit">Оформить заказ</button>
      </form>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      total: Number
    },
    data() {
      return {
        name: '',
        email: '',
        address: ''
      };
    },
    methods: {
      submitOrder() {
        if (this.total > 0) {
          alert(`Заказ оформлен! Имя: ${this.name}, Email: ${this.email}, Адрес: ${this.address}, Сумма: ${this.total}$`);
        } else {
          alert('Корзина пуста!');
        }
      }
    }
  };
  </script>
  
  <style>
  form {
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  
  div {
    margin-bottom: 10px;
  }
  
  button {
    margin-top: 10px;
  }
  </style>
  