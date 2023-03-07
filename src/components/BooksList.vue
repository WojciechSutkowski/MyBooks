<script setup lang="ts">
import { computed, PropType } from 'vue';
import BookTypes from '../types/BookTypes';
import OrderTerm from '../types/OrderTerm';

const props = defineProps({
  books: {
    type: Array as PropType<BookTypes[]>,
    required: true,
  },
  order: {
    type: String as PropType<OrderTerm>,
    required: true,
  },
});

const orderedBooks = computed(() => {
  return [...props.books].sort((a: BookTypes, b: BookTypes) => {
    return a[props.order] > b[props.order] ? 1 : -1;
  });
});
</script>

<template>
  <h4 class="order-info">Ordered by {{ order }}</h4>
  <TransitionGroup name="list" tag="ul" class="books__list">
    <li class="books__list__item" v-for="book in orderedBooks" :key="book.id">
      <img class="books__list__item--cover" :src="book.cover" />
      <header class="books__list__item--header">
        <h2 class="books__list__item--title">{{ book.title }}</h2>
        <h3 class="books__list__item--author">{{ book.author }}</h3>
      </header>
      <main class="books__list__item--main">
        <div class="books__list__item--rating">
          <i class="fa-sharp fa-solid fa-star"></i>
          <p class="books__list__item--rate">{{ book.rate }} / 10</p>
        </div>
        <p class="books__list__item--price">
          Bought for {{ book.price.toFixed(2) }} PLN
        </p>
        <p class="books__list__item--description">
          Lorem ipsum, dolor sit amet consectetur adipisicing elit. Fugiat amet
          maxime laudantium. Nobis obcaecati ipsum saepe quis eaque! Nobis
          beatae exercitationem porro unde voluptatem ipsa, dolorem error
          ducimus provident. Perferendis. Lorem ipsum dolor sit amet,
          consectetur adipisicing elit. Atque ratione eaque velit quia quam!
          Perspiciatis quasi suscipit accusantium consequuntur odit? Quisquam
          pariatur unde perferendis soluta itaque similique error veritatis
          minima!
        </p>
      </main>
    </li>
  </TransitionGroup>
</template>

<style lang="scss" scoped>
.order-info {
  padding: 1.2rem 0rem 0.6rem;
  font-size: 1.6rem;
  font-weight: 600;
}
.books__list {
  list-style: none;
  display: flex;
  flex-direction: column;
  gap: 1.2rem;

  &__item {
    display: grid;
    grid-template-columns: 1fr 3fr;
    grid-template-rows: 1fr 4fr;
    border-radius: 10px;
    overflow: hidden;

    -webkit-box-shadow: 10px 5px 5px -5px rgba(169, 169, 169, 1);
    -moz-box-shadow: 10px 5px 5px -5px rgba(169, 169, 169, 1);
    box-shadow: 10px 5px 5px -5px rgba(169, 169, 169, 1);

    &--cover {
      width: 100%;
      height: 100%;
      object-fit: cover;
      grid-column: 1/2;
      grid-row: 1/3;
    }

    &--header {
      background-color: #f0f0f0;
      padding: 1.2rem;
      color: black;
      display: flex;
      flex-direction: column;
      justify-content: end;
      gap: 0.2rem;
      border-bottom: 1px solid black;
    }

    &--title {
      font-size: 2.4rem;
      overflow-wrap: anywhere;
    }

    &--author {
      font-size: 1.4rem;
      font-weight: 400;
      color: #333;
    }

    &--main {
      background-color: #f7f7f7;
      padding: 1.2rem;
      display: flex;
      flex-direction: column;
      gap: 1rem;
    }

    &--rating {
      display: flex;
      font-size: 3.6rem;
      gap: 1rem;
      color: #f5b609;
    }

    &--rate {
      color: black;
      font-weight: 700;
    }

    &--price {
      padding: 1rem;
      background-color: #616467;
      width: fit-content;
      color: #e4e4e4;
      font-size: 1.4rem;
      font-weight: 500;
      border-radius: 5px;
    }

    &--description {
      color: black;
      font-size: 2rem;
    }
  }
}
.list-move {
  transition: all 1s;
}
</style>
