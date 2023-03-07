<script setup lang="ts">
import { ref } from 'vue';
import BookTypes from './types/BookTypes';
import OrderTerm from './types/OrderTerm';
import BooksList from './components/BooksList.vue';

const books = ref<BookTypes[]>([
  {
    title: 'Chrobot',
    author: 'Tomasz Michniewicz',
    cover:
      'https://ecsmedia.pl/c/chrobot-zycie-najzwyklejszych-ludzi-swiata-b-iext120839536.jpg',
    rate: 9,
    price: 40,
    id: '1',
  },
  {
    title: 'Kolej podziemna',
    author: 'Colson Whitehead',
    cover: 'https://ecsmedia.pl/c/kolej-podziemna-b-iext123090588.jpg',
    rate: 9,
    price: 39,
    id: '2',
  },
  {
    title: 'Sapiens',
    author: 'Yuval Noah Harari',
    cover:
      'https://image.ceneostatic.pl/data/article_picture/d0/3a/8272-c606-4c9c-a8e5-2b6d8a440ccc_large.jpg',
    rate: 7,
    price: 50,
    id: '3',
  },
]);

const order = ref<OrderTerm>('title');

const handleSort = (term: OrderTerm) => {
  order.value = term;
};
</script>

<template>
  <header class="header">
    <i class="fa-solid fa-book-open header__icon"></i>
    <h1 class="header__name">MyBooks</h1>
  </header>
  <nav class="nav">
    <button class="btn" @click="handleSort('title')">Order by title</button>
    <button class="btn" @click="handleSort('author')">Order by author</button>
    <button class="btn" @click="handleSort('rate')">Order by rate</button>
    <button class="btn" @click="handleSort('price')">Order by price</button>
  </nav>
  <BooksList :books="books" :order="order" />
  <footer class="footer">
    <p>
      Copyright &copy; <span class="year">2023</span> &#124; Wojciech Sutkowski
      &#124; All rights reserved.
    </p>
  </footer>
</template>

<style lang="scss" scoped>
.header {
  display: flex;
  gap: 0.2rem;
  justify-content: center;
  align-items: end;
  padding: 2rem;

  &__icon {
    font-size: 3.6rem;
  }

  &__name {
    font-family: 'Julius Sans One', sans-serif;
    font-size: 3.2rem;
  }
}

.nav {
  display: flex;
  justify-content: space-evenly;
}

.btn {
  display: inline-block;
  outline: none;
  cursor: pointer;
  font-size: 1.4rem;
  line-height: 1;
  border-radius: 500px;
  transition-property: background-color, border-color, color, box-shadow, filter;
  transition-duration: 0.3s;
  border: 1px solid transparent;
  letter-spacing: 2px;
  min-width: 16rem;
  text-transform: uppercase;
  white-space: normal;
  font-weight: 700;
  text-align: center;
  padding: 1.6rem 1.4rem 1.8rem;
  color: #616467;
  box-shadow: inset 0 0 0 2px #616467;
  background-color: transparent;
  height: 48px;

  &:hover {
    color: #fff;
    background-color: #616467;
  }
}

.footer {
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1.4rem;
  padding: 2.4rem 0;
}
</style>
