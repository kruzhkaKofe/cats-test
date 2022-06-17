<template>
  <div class="app">
    <div class="inner-wrapper">
      <page-header />
      <div class="card-wrapper">
        <product-card :cards="cards" />
      </div>
    </div>
  </div>
</template>

<script>
import ProductCard from "@/components/ProductCard";
import PageHeader from "@/components/PageHeader";

export default {
  components: {
    ProductCard,
    PageHeader,
  },

  data() {
    return {
      cards: [
        {
          id: "1",
          sort: "с фуа-гра",
          sklad: "Печень утки разварная с артишоками.",
          volume: ["10 порций", "мышь в подарок"],
          weight: "0,5",
          available: true,
        },
        {
          id: "2",
          sort: "с рыбой",
          sklad: "Головы щучьи с чесноком да свежайшая сёмгушка.",
          volume: ["40 порций", "2 мыши в подарок"],
          weight: "2",
          available: true,
        },
        {
          id: "3",
          sort: "с курой",
          sklad: "Филе из цыплят с трюфелями в бульоне.",
          volume: ["100 порций", "5 мышей в подарок", "заказчик доволен"],
          weight: "5",
          available: false,
        },
      ],
    };
  },
};
</script>

<style lang="sass">
*
  margin: 0
  padding: 0
  box-sizing: border-box

li
  list-style: none

html, body
  height: 100%
  width: 100%

body
  font-family: 'Trebuchet MS', sans-serif
  font-weight: 400
  background: linear-gradient(180deg, rgba(0, 0, 0, 0.5) 0%, rgba(0, 0, 0, 5e-05) 49.88%, rgba(0, 0, 0, 0.5) 100%), url('@/assets/main-bg.png')

.app
  height: 100vh
  display: flex

.inner-wrapper
  padding: 20px 0
  margin: auto
  width: 1200px

.card-wrapper
  display: flex
  justify-content: center
  flex-wrap: wrap
</style>
